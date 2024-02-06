# 2. Essential Math and Data Science

* Data science basics
* Optimization and heuristics
* ML and AI in practice

## 2.1 Data Science Basics

### Key Terms

* **Jupyter Notebook:** A web application to create and share documents containing live code, visualization and text.
* **Colab Notebook:** Google-hosted version of Jupyter Notebook.
* **Github:** A Git repository service for storing and managing code, and tracking changes.
* **Virtual Environment:** An isolated Python environment.
* **README file:** A text file that introduces and explains a project.
* **requirements.txt:** A text file listing all the Python package dependencies needed for the application.
* **Makefile:** A file containing a set of directives to automate building, testing, and managing a project.
* **Continuous Integration:** The practice of frequently merging code changes, and automatically building and testing code.



### What A Data Scientist Does

* **Ingest:** Get the data.
* **Exploratory Data Analysis (EDA):** What data you're dealing with.
* **Modeling:** Test your hypotheses.
* **Conclusion:** Does the data back up your hypotheses.

Format your notebooks like this.

---

**Note:** If you have a notebook in your repo and want automated testing for it, do the following:

```makefile
# Makefile
install:
	pip install --upgrade pip && pip install -r requirements.txt
	
test:
	python -m pytest --nbval notebook.ipynb
```

The `--nbval` runs every cell in the notebook and makes sure they're valid.

---



## 2.2 Optimization, Heuristics, and Simualation

### Key Terms

* **Heuristic:** A practical problem-solving approach, not guaranteed to be optimal but sufficient for reaching an immediate goal.
* **Greedy algorithm:** An algorithm that follows the heuristic of making locally optimal choices at each stage.
* **Simulation:** Imitating a real-world process over time with a mathematical model to study behavior and performance.
* **Law of Large Numbers:** The principle that the larger the sample size in a probabilistic simulation, the more it reveals the true underlying statistical distributions.
* **Experiment Tracking:** The MLOps practice of tracking key metrics like performance across iterations of an ML experiment.

---

To fully understand how to build heuristics, meta heuristics, and algorithms, let's go over **Traveling Salesman Problem (TSP)**. In this problem, you're supposed to visit all of the cities with minimum cost.

* Greedy algorithm: At every point, pick the city closest to you.
* Simulation: pick random starting points and see how your agent acts.



**Experiment Tracking** is very much like **simulations**. We want to minimize error metric through hyperparameter tuning.

---



## 2.3 Machine Learning and AI in Practice

### Key Terms

* **Supervised learning:** A type of machine learning using labeled data to train models to predict unlabeled data.
* **Unsupervised learning:** A machine learning apporach that finds hidden patterns and relationships in unlabeled data.
* **Clustering:** An unsupervised learning technique that groups data points based on similarity.
* **K-Means clustering:** A clustering algorithm that partitions data into _k_ clusters by computing the mean of all data points assigned to a cluster.
* **Diagnostics:** Visual tools like _elbow plots_, _sihouette analysis_, and _distance maps_ used to evaluate and tune the performance of clustering models.
* **Parallelization:** Running clustering computations like K-Means concurrently across multiple CPUs to improve performance.



For **paralleization** you need a machine with many CPU cores. For that,

* Go to AWS > Cloud9
* Create an environment (name it "BigEnvironment")
* Get an EC2 instance with 32 CPUs
* "create environment"