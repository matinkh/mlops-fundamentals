# 3. Operations Pipelines: DevOps, DataOps, MLOps

In this part, we'll cover

1. Github Ecosystem
2. Using pipelines for DataOps
3. Functions - zero to deploy

## 3.1 Github Ecosystem

### Key Terms

* **Codespaces:** Cloud-based environment hosted by GitHub.
* **Reproducibility:** The ability to reliably recreate an environment and obtain the same results. (Codespaces ensure this through containers)
* **Container image:** A lightweight, stand-alone, executable software package allowing code to run quickly and reliably across environments.
* **Copilot:** GitHub's AI pair programmer.
* **Continuous integration:** The development practice of frequently merging code changes and validating each change through automated build and test processes.
* **Continuous delivery:** Software methodology where teams can release new changes to users quickly and reliably through automated deployments.



#### Cloud Dev Workspaces

* **GitHub Codespaces**
  * OpenAI codex
  * GitHub Copilot
  * GitHub actions
* **AWS Cloud9**
* **GCP Cloud IDE**
* **Azure Cloud IDE**



#### The benefits of Cloud Dev Workspace

Working on a laptop/workspaces come with some cons:

* Non-deterministic
* Costs
* Not same as deploy env

While working on cloud-dev workspaces come with

* GPUs
* access control
* service integration (e.g., with AWS S3, ...)



#### GitHub for MLOps

Why using GitHub Workspaces?

* **Reproducibility:** Codespaces allows that through i) container image, ii) configuration, and iii) compute and storage.
* **Access to GPU** which is required for ML models.
* **AI Coding Assistant:** you can use Copilot for lint, test, format, ...
* **CI/CD:** GitHub Actions
  * CI: `make install`, `make test`, `make deploy`
  * CD: `sync with cloud` (Amazon ECR, HuggingFace hub)

Also, you can use **templates** to setup your GitHub repository with predefined `devcontainer`, _actions_, etc.



#### Fine-Tuning with Hugging Face

[Hugging Face](huggingface.co) is a model hosting service that has three main components:

1. **Models:** list of models, tagged with their tasks and usecases.
2. **Datasets:** list of available data for a variety of purposes.
3. **Spaces:** deploy ML models for demos.



## 3.2 Using Pipelines for DataOps

### Key Terms

* **AWS Setup Functions:** A serverless orchestration service that lets you coordinate components of distributed microservices.
* **AWS Batch:** A managed computing service that schedules and runs batch computing workloads of any scale on AWS.
* **AWS Glue:** A serverless ETL and data integration service that prepares and transforms data.
* **ETL Pipeline:** Extract, transform, load pipelines that pull data from srouces, processes them, and load them into a destination database or data warehouse.
* **Serverless Pipeline:** Using cloud services like Lambda, Glue, Batch, and Step Functions to build data pipelines that automatically manage infrastructure.
* **DataOps:** Data management practices focused on improving the quality and speed of data delivery by automating infrastructure.



### Pipelines for DataOps using Step Functions

We can create a **workflow** using AWS Lambda and Step Functions.

* **Lambda:**

  * Go to AWS Lambda and **create a function**

    * You can specify a _trigger_ and _destination_ too

  * It will generate`lambda_function.py` that has the following function:

    ```python
    def lambda_function(event, context):
      if event["param1"] == True:
        return {"StatusCode": 200, "body": json.dumps(f"The parameter received")}
      # ...
    ```

    * `event` is a json string, which is a dict in Python.

  * To setup a test input, you "_create new event_" and specify what the input `event` is.

  * The successor Lambda function receives the output of this function; should parse `event["body"]` for parameter.

* **Step Function:**

  * Go to AWS Step Functions to coordinate the workflow.
  * You (can) visually arrange the tasks (Lambda functions). For each Lambda, you select the ones you implemented.
  * Name your **state machine**.
  * Start execution

The whole chain of tasks is similar to **unix-style chain of commands** - i.e., their inputs and outputs are standardized and can be chained.
