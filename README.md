# Helsinki Machine Learning Project Template
> Template for open source ML and analytics projects.


## About This Template

This is a git repository\* template for Python-based open source ML and analytics projects.

---
** INFO BOX: Git Repository ** 
\*A git repository is a folder that contains source code and documentation for a software project.
Git is a software for version control and collaborative coding work. 
Git is commonly used from from command prompt (Windows), shell (Linux / Ubuntu) or terminal (MacOS).
It keeps track of all changes you make to your software in a `.gitfile`,
so that you can try out different things without making messy manual back ups.
To learn more about Git, their [homepage](https://git-scm.com/) is a great place to start.
Git is often used with GitHub, a free online service for storing and sharing repositories.
GitHub allows collaborative work, automated testing, hosting project doc pages and other fancy features.
Read more on GitHub on their [homepage](https://github.com/City-of-Helsinki/ml_project_template).

---

This template helps you to develop, test, share and update ML applications.
It defines steps and tools of a ML project and helps you to tie them together for easy to use, explainable and reproducible workflow.
You can just replace the examples with your own code, or start from scratch with clean notebooks.
Instructions for using the template are given below, so just keep reading!

The template is completely open source and environment agnostic.
It contains examples and instructions to help you through the whole project.
However, we try to keep it light and easy to maintain, and thus the documentation is not exhaustive.
We have added references to original sources so that they are easy to find.

If you see a tool or concept you are not familiar with, don't be scared.
Just follow along and you'll get started with ease, for sure.

If you have a question, the internet most probably already has the answer. Just search engine it!
If you can't find the answer, you can post your question to the [discussion forum](https://github.com/City-of-Helsinki/ml_project_template/discussions),
so the maintainers can help. [Stack Overflow](https://stackoverflow.com/) is the recommended forum for questions that are not specific to this template.

All you need to do for starting to work on your data project is to install the template following the instructions below.


## Principles of the Template

The template follows four guiding principles.
Remember, none of these are strict and you are free to deviate for achieving the best results for you.
Also, it is better to get started with the work than to perfect it from the beginning.
You may return to these concepts when you want to improve your project or get stuck, iteratively!

### 1. Exploratory Programming - Use Jupyter Notebooks

We want to keep our code, documentation and results together, seamlessly.
We also want to see what's going on as we create the software, immediately.
That's why we use jypyter notebooks as the core of our development.

Actually, even this page was generated from a notebook!

The notebooks are enhanced with `nbdev` tool to export code to modules, create doc pages, run tests, handle notebook version control etc.

Some reasoning for those who are not yet convinced:

- In data projects, the code efficiency is irrelevant. The thinking time is what matters.
- It is simply impractical to create poorly documented notebook. With notebook development, your code is always well documented.
- How many of you actually test your ML code? Clean, running notebooks are the tests, and with `nbdev` unit tests are easy to include. 
- Most data science projects involve multiple stakeholders with various backgrounds and skillsets.
Many of them do not understand code, and even those who do, can not if it is poorly documented, nor can they interpret the results alone.
Notebook development can be used to improve explainability.
- If you are building an armada of spaceships, tiny IoT devices or otherwise feel that this template does not fulfill your requirements for production pipeline,
you can still use this for planning and creating documentation. Clean code is easier to achieve following a well documented demo!

With notebook development you get the right results much faster, and everyone involved can actually understand what is happening.

Read more on exploratory programming with notebooks from [this blog post](https://www.fast.ai/2019/12/02/nbdev/).

Read more on nbdev on their [project pages](https://nbdev.fast.ai/).

### 2. Ease of Reproducibility

Poor reproducibility is a major issue in data science projects, both in the industry and academia, but is often overlooked at.
We at the city of Helsinki, as a public sector operators, value it highly, and believe that everyone will benefit from it.
Our goal is, that each state and decision of our ML models are reproducible.
A theoretical possibility of recreating a particular result is not enough, if it takes unreasonable efforts to do it.
Good reproducibility equals to ease of reproducibility.

For ease of reproducibility we 

1. Document
2. Seed
3. Orchestrate (pipeline)
4. Version control everything.

--- 
** INFO BOX: Documentation, Seeding, Orchestration and Version control **

*Documentation*

Documentation means, that everything in a ML project is explained in a text (up to a reasonable level).
This includes commenting code, but also adding relevant references, explaining the maths if needed, and introducing the logic and reasoning between every step.
To help you with documentation, you can ask yourself "what am I doing and why?" when coding,
and "what does this mean?" every time you get results, be it an intermediate step in data cleansing or the final results of your workflow.
Then, write the answers down, and ask your *non-tech-savvy* colleague to explain the process and results to you based on your documentation.
Iterate this, until you are happy with their answer, and you'll have great documentation!
With great documentation you can ensure that someone else could actually reproduce the same results you came up with.

*Seed*

Seeding means, that random processes are initialized with a *seed*, also known as *random state*.
Creating random numbers is a difficult task in computer science. Each random number you get from a random number generator,
such as the `np.random`, is actually a *pseudo random* number - number taken from a number sequence.
Bunch of numbers taken from this sequence have properties similar to some taking them from true random distribution.
The sequence is defined by the initial number, the seed, and so if you use the same seed for a random number generator,
you can reproduce the results.

*Orchestration*

Orchestration or *pipeline* means automated workflow control.
The goal is, that with a single command you can run all steps of your workflow,
instead of trying to rerun individual cells or notebooks.
It means, that with the same code and same data,
you can always reproduce the same results, even if your code isn't all in a single script.
It helps you to automate the training of ML models in production,
but also when testing your model in development.
An orchestrated workflow is excecuted on a trigger event.
They can either be static or dynamic. A static workflow executes all steps on the trigger event.
Most applications have static workflows.
This is ok, if you have a static data source (the data can change) and your processing steps are computationally light.
Dynamic workflows only execute the steps that are required, i.e. the steps,
that are affected by the changes that happened since the last trigger event.
This change can either be in the code or in the data.
For example if you may have a varying number of input sources to read data from at each training round of the algorithm.
Depending on your ML application, you should consider if you want to use static or dynamic orchestration.
We will add examples of both in the `pipe` notebook.

*Version control*

Version control means that you keep track of all changes in your system,
in a reversable way that allows you to step back to a previous version, or make branches to try out options.
Version control allows you to refer to a specific version of your system, making these snapshots reproducible.
We use Git for version control of code. Data version control is a topic we are still working on.

---

### 3. Tidy Data & Tools

Tidy principles are guidelines for clean and efficiend data utilization.
They can be appied to different programming languages.
Common packages, like `numpy`, `pandas` and `sklearn` have been developed so that these concepts are easy to apply.
Tidy data is easy to handle and understand. Tidy tools makes handling data, programming and creating explainable ML much easier.

**Data is tidy, when:**

1. **Every column is a variable** (either a feature or a label)
2. **Every row is an observation** (a data point).
3. **Every cell contains a single numerical value** (int, float, bool, str*)
> *strings should be converted to numerical format before applying ML

Read more on tidy data from [tidy data manifesto](https://vita.had.co.nz/papers/tidy-data.html).

**Tidy Tools:**

1. **Reuse existing data structures**

Favour the default data types of the tools used over custom data types.
Avoid unnecessary conversions: once you have converted your data to tidy format, keep it tidy.

2. **Compose simple functions with the pipe**

A pipe operator takes the expression before it and gives it as the first argument to the expression after it,
assuming the expression on the right is a function call. In addition, pipe functions should do one thing, and do it well.
They either perform a transformation or a side-effect, but never both.

In a transformation a modified copy of the input is returned.
In a side effect a reference to the directly modified input is returned.

This allows composition of simple functions. In addition, you can easily determine what a pipeable function does just from its name.
In pseudocode, it looks something like this

```
model() >> init(X_train, y_train) >> fit(hyperparam) >> predict(X_test) >> mean()
```

instead of multiple lines of code

```
m = model()
m>init(X_train, y_train)
m>fit(hyperparam)
prediction = m>predict(X_test)
mean_values = prediction>mean()
```
although you can use pipeable functions in either way, or as a composition.

Piped code is easy to read: you see that a model class is initialized, fitted with certain hyperparameters, a prediction is made and aggregated to a mean.
Python does not have a native pipe operator such as `%>%` in R tidyverse,
but Python class functions can be written in a pipe-like way.
More on this in the `model` notebook.

As an excercise, you can take a look at function definitions of your favourite `sklearn` model.
Which of the functions perform transformations and which side-effects?
Can you find a function that does both?

3. **Embrace functional programming**

Python is not a functional programming language, but it can be written in functional style.
Many of the concepts can be used to write cleaner data code with Python. 
Read more on functional programming with Python from [this Stack Abuse article](https://stackabuse.com/functional-programming-in-python).

4. **Are designed for humans**

In addition to clean structure and documentation, consider the naming of your classes, functions and variables.
Clean code is easy to understand, and actually eases your work with the documentation. 
Function name should describe what it does.
A lengthy informative names is better than short, uninformative ones.
Having a common prefix with similar functions and autocomplete makes make even lengthy names descriptions easy to use. 

Read more on tidy tools from [tidy tools manifesto](https://cran.r-project.org/web/packages/tidyverse/vignettes/manifesto.html).


### 4. Data, Model & Loss - The Three Components of Machine Learning

The core of this template constitutes of three notebooks: data, model and loss.
The notebooks running number prefix (`00_data.ipynb etc.) to emphasize the running order and to improve readability.
Any data project can be resolved by defining these three steps.

You might be used to doing all of them in a single script (multiple lines of code in a file, excecuted in order from top to bottom),
but separating makes development, explaining the results and debugging much more efficient. 

Each notebook is also a basis for a python module, including tests and documentation.
The `nbdev` tool constructs a python module of each of these notebooks, under the folder `[your git project name]` (`ml_project_template` in this template).
This allows you to share code between your notebooks, or even publish a complete python module, while doing all your development in the notebooks.

**Data**

In the data notebook, the the data is loaded and cleaned, and a basic analysis may be carried out.
With nbdev you can also export data handling functions to be used in other notebooks.
You should also create a small toy dataset to develop and test your algorithm with - no,
trust me, your code won't work for the first n+1 times, and running it with the whole dataset will waste so much time!
This is also why we separate between the model and loss notebooks.

**Model**

In the model notebook, the machine learning model (or analytics or simulation) is explored, defined and tested.
You can begin with scripting, but based on the script you should develop real generalizable and tested code.
This part of the notebooks is the closest to traditional software development it gets: the output is a clean Python module. 

**Loss**

In the loss notebook, you will finally train your model with the whole dataset and evaluate it in action.
Some might call this step *inference*, others *evaluation*.
No matter the name, you evaluate the performance of your model to see if it is ready for production.
If the results are satisfactory, you can ship your code to it's destination.
For example Azure SDK allows you to define your code in Python and then excecute it in the cloud, seamlessly.
However, this part depends a lot on the project, so we'll leave it to you to figure it out.
If your are doing research, having the results in the notebooks might be enough for you.

Currently, these notebooks will have to be run manually.
We will soon include additional tools `papermill` and `snakemake`,
and a third notebook `pipe` for automatical excecution of the workflow.

You can also create new notebooks to your liking. We added one example: `plot`, where we can define general functions for plotting.

For general coding best practices, refer to [dev.hel.fi](https://dev.hel.fi/) where applicable.

## Example Project

We wanted to make this template easy to approach.
That's why we included a demo, that it is built around.

The demo is an example ML project on automating heart disease diagnosis with logistic regression on [UCI heart disease open dataset](https://archive.ics.uci.edu/ml/datasets/heart+disease).
The dataset contains missing values, and is thus great for demonstrating some light data wrangling.
The demo is only meant for showcasing how the template joins together different tools and steps.

**If you'd like to skip the demo**, and get right into action, you can replace the notebooks `index`, `data`, `model` and `loss` with clean copies under `notebook_templates`.

The `index` notebook (this notebook or the empty copy) will become the `README` of your project and frontpage of your documentation, so edit it accordingly.
You should at least have a general description of the project,
instructions on how to install and use it,
and instructions for contributing.

## Installing the template
{% include note.html content='if you are doing a project on personal or sensitive data for the City of Helsinki, contact the data and analytics team of the city before proceeding!' %}
### On your GitHub homepage:

1. Sign into your GitHub account
2. In the top right corner of the homepage, click the '+'-button
3. Select 'Import repository'
4. Under 'Your old repository's clone URL' copy the clone url of this repository: `https://github.com/City-of-Helsinki/ml_project_template`
5. Give your project a name. Do not use the dash symbol '-', but rather the underscore '_', because the name of the repo will become the name of your Python module.
6. Select owner of the repo, if you want to use the template for your organization.
Also define your project publicity (you can change this later, in most cases you'll want to begin with a private repo).
7. Click 'Begin import'

This will create a new repository for you copying everything from this template, including the commit history.

### On your computing environment:

**Put all the highlited **(`this is command`) ** commands to shell (replace the parts with square brackets with your own information '[]')**

0. Open shell, and move to the folder you want to work in: `cd [path to your programming projects folder]`.
(If you get lost, `cd ..` moves you one folder towards root, and `cd` gets you to root.)
1. Clone the repository you just imported: `git clone git@github.com:[repository owner]/[repository name]`.
This will copy all the files and folders that you imported to your new repository in the github website, to your computing environment.
2. Go inside the repository: `cd [repository name]`
3. Create virtual environment with dependencies, activate it, and create a ipython kernel for running the notebooks (This is designed for Helsinki developers, you may change this according to your system and preferences):
```
conda create --name [your project env name]
conda activate [your project env name]
conda install pip
pip install -r requirements.txt
nbdev_install_git_hooks
python -m ipykernel install --user --name [your ipython kernel name] --display-name "Python [python version] ([your ipython kernel name])"
```
5. Edit `settings.ini`, `docs/_config.yml` and `docs/_data/topnav.yml` according to your project details.
You can continue editing them in the future, so no need to worry about getting it right the first time.
These are used for building the python modules and docs based on your notebooks, so if you get weird errors there, take a look again at these files.
4. Configure your git user name and email adress (one of those added to your git account) if you haven't done it already:
```
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email "MY_NAME@example.com"
```
5. Make initial commit:
```
git add .
git commit -m "Initial commit"
```
6. Push: `git push -u origin master`

To use git with remote repository, you must create an ssh key and upload it to your git profile settings.
See [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) how to do it.
Then, you can push the commits to remote repository, where they are safe and allow collaborative work on the project.



## How to use

1. Install this template as basis of your new project (see above)

2. Check out the notebooks, and play around a bit to see that your installation works (notebooks run smoothly) and you understand the template structure

3. Edit the notebooks `index`, `data`, `model` and `loss` directly or replace them with empty notebooks clean of the code examples found in the folder `notebook_templates`.

4. You may delete `ml_project_template`, `notebook_templates` folders and the extra notebook `plot` if you no longer need them.
Use `git rm -r [folder name]` to also remove the folders and git tracking.

5. Save your notebooks and call `nbdev_build_lib` to build python modules of your notebooks - needed if you want to share code between notebooks or create a modules.
Remember to do this if you want to rerun your workflow after making changes to exportables. 

6. Save your notebooks and call `nbdev_build_docs` to create doc pages based on your notebooks (see below).
This will also create README.md file based on this notebook.
If you want to host your project pages on GitHub, you will have to make your project public.
You can also build the pages locally with `jekyll`.

7. Remember to track your changes with git! 

---

**INFO BOX: Some useful commands with git**

See which files have changes since the last commit: `git status` 

Add files to a commit: `git add [file names/paths separated by whitespace ' ']`

Create commit: `git commit -m "[short description of the changes you made]"`

Push commit to remote repository (GitHub server): `git push origin -u` 

Remove files so that git will also stop tracking them `git rm [file name]`

To ignore files or folders from being tracked by git, add them to `.gitignore` file.
In this template the `data` and `results` folders have been added to the `.gitignore`.
We do not want to version them with git, as it will explode the size of the repository. 

In addition, there are many fancy features for git that enable comparing differences, collaborative work, debugging, automated testing and other crazy things.
However, there are better sources for learning all that stuff.

---



## Contributing

## Now you are all set up and ready to begin you ML project!
