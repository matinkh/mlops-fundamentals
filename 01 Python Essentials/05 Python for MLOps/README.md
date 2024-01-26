# 5. Applied Python for MLOps

What's covered:

* Working with Azure and Hugging Face APIs and SDKs
* Automation with Command-Line Tools
* Building ML APIs



## 5.1 Working with APIs and SDKs

### Key Terms

* **Azure CLI:** A command-line tool that allows management and interactions with Azure services.

  ```python
  import azure.cli.core
  
  cli = azure.cli.core.AzureCli()
  cli.invoke(["storage", "account", "list"])
  ```

* **Azure ML Studio:** A cloud-based environment for ML development and deployment.

  ```python
  from azureml.core import Workspace
  
  ws = Workspace.create(name="myworkspace",
                       subscription_id="...",
                       resource_group="myresourcegroup",
                       location="westus")
  ```

* **Transformers:** A Hugging Face library for natural language processing tasks.

  ```python
  from transformers import pipeline
  
  classifier = pipeline("sentiment-analysis")
  result = classifier("I love this task")
  print(result)
  ```

* **Datasets:** A Hugging Face library for loading datasets.

  ```python
  from datasets import load_dataset
  
  dataset = load_dataset("glue", "mrpc")
  train_dataset = dataset["train"]
  print(len(train_dataset))
  ```

* **Open Datasets:** An Azure resource for loading public datasets.

  ```python
  from azureml.opendatasets import PublicHolidays
  
  holidays = PublicHolidays()
  holidays_df = holidays.to_pandas_dataframe()
  print(holidays_df.head())
  ```

  

## 5.2 Automation with Command-Line Tools

### Key Terms

* **Click:** A Python package for building command line interface.

  ```python
  import click
  
  @click.command()
  @click.option("--count", default=1)
  def hello(count):
    for _ in range(count):
      click.echo("Hello World")
      
  if __name__ == "__main__":
    hello()
  ```

* **ArgParse:** A Python module for parsing command-line arguments.

  ```python
  import argparse
  
  parser = argparse.ArgumentParser()
  parser.add_argument("--verbosity", action="store_true")
  args = parser.parse_args()
  
  if args.verbosity:
    print("Verbose mode enabled")
  ```

* **sys.argv:** A Python module containing command-line arguments.

  ```python
  import sys
  
  print(f"Script name: {sys.argv[0]}")
  print(f"First argument: {sys.argv[1]}")
  ```

* **Setuptools:** A package for building and distributing Python projects.

  ```python
  from setuptools import setup
  
  setup(
    name="mypackage",
    version="1.0",
    install_requires=["requests", "click"]
  )
  ```

* **Entry points:** Definitions linking scripts to functions in Setuptools.

  ```python
  from setuptools import setup
  
  setup(
    #...,
    entry_points = {
      "console_scripts": ["myscript = mypackage.mymodule.main_func"]
    }
  )
  ```



##### Packaging your Project

To do that, you need `setup.py` in your project's root directory like

```bash
Repo
 |---jformat/
        |----main.py
 |---.gitignore
 |---README.md
 |---setup.py
```

```python
from setuptools import setup, find_packages

setup(
  name="jformat",
  version="0.0.1",
  description="Reformats fiels to stdout",
  install_requires = ["click", "colorama"],
  entry_points="""
  [console_scripts]
  jformat=jformat.main:main
  """
  author="Matin K",
  author_email="matink@...",
  packages=find_packages(),
)
```

Now, we can install it in our venv/bin library by:

```bash
$ python setup.py develop
```



##### Solving an ML Problem with a CLI Tool

```bash
HUGGINGFACE-SUMMARIZATION
  |---summarize/
         |---main.py
  |---.gitignore
  |---README.md
  |---requirements.txt
  |---setup.py
```

Inside `requirements.txt`, we'll include our dependencies:

```
transformers==4.21.2
click==7.1.2
tensorflow==2.9.1
```

In `summarize/main.py` we have

```python
import click
from transformers import pipeline
import urlib.request
from bs4 import BeautifulSoup
import os
os.environ['TF_CPP_MIN_LOG_LEVEL'] = "3"

def extract_from_url(url):
  """Returns contents of a webpage as plain text
  """
  
def process(text):
	summarizer = pipeline("summarization", model="t5-small")
  result = summarizer(text, max_length=180)
  click.echo("Summarization process complete")
  click.echo("=" * 80)
  return result[0]["summary_text"]

@click.command()
@click.option("--url")
@click.option("--file")
def main(url, file):
  if url:
    text = extract_from_url(url)
  elif file:
    with open(file, "r") as f:
      text = f.read()
  click.echo(f"Summarized text from {url or file}")
  click.echo(process(text))
```

In `setup.py`:

```python
from setuptools import setup, find_packages

with open("requirements.txt", "r") as f:
  requirements = [line for line in f.read().split("\n")]
  
setup(
  name="summarize",
  description="Python CLI tool to summarize text",
  packages=find_packages(),
  author="Matin K",
  entry_points="""
  [console_scripts]
  summarize=summarize.main:main
  """
  install_requires=requirements,
  version="0.0.1",
  url="https://github.com/matinkh/..."
)
```

```bash
$ python setup.py develop
```

Now our package is ready to solve an ML problem - summarization!

```bash
$ summarize --url="https://blog.google.com"
```



## 5.3 Building Machine Learning APIs

### Key Terms

* **FastAPI:** A Python web framework for building APIs.

  ```python
  from fastapi import FastAPI
  
  app = FastAPI()
  
  @app.get("/")
  def read_root():
    return {"message": "Hello World"}
  
  print(read_root())
  ```

* **Flask:** A lightweight Python framework.

  ```python
  from flask import Flask
  
  app = Flask(__name__)
  def home():
    return "<h1>Home Page</h1>"
  
  if __name__ == "__main__":
    app.run()
  ```

* **Transform:** Hugging Face library for NLP tasks.

  ```python
  from transformers import pipeline
  
  classifier = pipeline("sentiment-analysis")
  result = classifier("I love blogging")
  print(result)
  ```

* **Onyx:** ML model server for high-performance inferencing.

  ```python
  import onnxruntime as rt
  
  sess = rt.InferenceSession("model.onnx")
  input_name = sess.get_inputs()[0].name
  res = sess.run(None, {input_name: x})
  ```

* **OpenAPI:** Specification for API documentation.

  ```python
  from fastapi import FastAPI
  from fastapi.openapi.utils import get_openai
  
  app = FastAPI()
  
  def custom_openapi():
    return get_openapi(
      title="My API",
      version="1.0.0",
      description="Some description",
    )
    
  app.openapi = custom_openapi
  ```



We'll cover how to build HTTP APIs for our ML models. We cover two options

* **Flask?**
* **FastAPI** (not covered here)

### 5.3.1 Flask

```python
from flask import Flask, abort

app = Flask(__name__)

# If my address is "example.com", the following is "example.com/"
@app.route("/")
def two_hundred():
  return "<h1>200! All is good</h>"

@app.route("/error")
def error():
  abort(500, "Something went wrong")
  
if __name__ == "__main__":
  app.run(debug=True, port=80, host="0.0.0.0")
```

Now, let's do a quick _sentiment analysis_ with $\texttt{RoBERTa}$.

```python
from flask import Flask, request, jsonify
import torch
from transformers import RobertaTokenizer
import onnxruntime


app = Flask(__name__)
tokenizer = RobertaTokenizer.from_pretrained("roberta-base")
session = onnxruntime.InferenceSession("roberta-sequence-classification-9.onnx")

@app.route("/")
def home():
  return "<h2>RoBERTa sentiment analysis"

@app.route("/predict", methods=["POST"])
def predict():
  input_ids = torch.tensor(tokenizer.encode(request.json[0], add_special_tokens=True)
                          ).unsqueeze(0))
	inputs = {session.get_inputs()[0].name: to_numpy(input_ids)}
  out = session.run(None, inputs)
  result = np.argmax(out)
  return jsonify({"positive": bool(result)})

if __name__ == "__main__":
  app.run(host="0.0.0.0", port=80, debug=True)
```

Now you can interact with this application using curl:

```bash
$ curl -K POST --header "Content-Type: appliction/json" --data '["Flask is useful"]' http://127.0.0.1:80/predict
>>> "positive": true
```

### 5.3.2 FastAPI

Very similar to Flask. But now you have to implement the app following certain guidelines. 



### 5.3.3 Python API Best Practices

* HTTP Error Codes
  * `400 Bad request`
  * `401 Unauthorized`
  * `404 Not found`
* Request types
  * GET: Read Only
  * POST: Write Only
  * PUT: Update existing
  * HEAD: Does it exist?

