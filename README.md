# Set Up

## Summary

This set-up section will document the following:

1) Creating a new python / anaconda environment for package versioning and dependencies.

2) Set up VSCode to run `.ipynb` notebooks.

3) Connecting an `.ipynb` notebook in VSCode to a Databricks cluster.

## Environments

Environments are used to control package versions and dependencies across projects. Each project should have their own environment, to allow different projects to use different versions of the same package. There are generally two ways to create an environment:

**Option 1: Python Virtual Environments**. Python virtual environments are natively supported by python. To create a python virtual environment:

1) Navigate to your project folder.

2) In a bash terminal, run the command `python -m venv <name of environment>`, where `<name of environment>` is replaced with your choice of name. Note that the most common choice is the name `.venv`.

3) Activate the virtual environment with the command `source <name of environment>/bin/activate` (on POSIX systems) or `source <name of environment>/Scripts/activate` on Windows. If you are on a bash terminal, the name of the environment should appear in parenthesis to the left of the command line. NOTE: the environment deactivates everytime the terminal is closed, so we will need to activate the environment everytime we boot up a fresh instance of the terminal.

4) With the environment activated, we install packages using `pip`. The packages will be installed to the specific environment and only accessible by that environment. This helps silo each package version to a specific project.

5) Once the environment is activated, packages can be installed using the command `pip install <package name>`.

Further documentation can be found here <a href="https://docs.python.org/3/library/venv.html">venv - Creation of virtual environmnets</a>.


**Option 2: Conda Environments**. Anaconda also allows for environment creation and package management. To create a new anaconda environment:

1) Navigate to your project folder.

2) In bash terminal, run the command `conda create --name <name of environment>`. The choice of name is typically the project's name. You will prompted to proceed `proceed ([y]/n)?`. Type and enter `y` into the terminal to proceed.

3) Activate the environment with the command `conda activate <name of environment>`.

4) Once the environment is activated, packages can be installed using `conda install <package name>`.

Note: this same process can be done with the GUI in Anaconda Navigator. Further documentation can be found here <a href="https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html"> Managing environments - conda </a>.

This repo uses an `conda` environment for package managment. The exact state and package versions used in the environment is stored in the `environment.yml` file, which can be used to recreate the exact conda environment used in the repo. Do this by running the command:

`conda env --name <name of your env> --file environment.yml --prune`

<br>

## VS Code

VS Code is text-editor used to write code in any language. Various plug-ins can be downloaded and installed for any kind of specialized functionality, making VS Code a good choice for an all-in-one IDE for projects requiring multiple different programming langauges.

One main advantage of VS Code is that it natively supports `.ipynb` notebooks aka iPython / Jupyter notebooks. Here is the general workflow for using Jupyter notebooks via VS Code:

1) Activate your project's environment and install the `jupyter` package using either `pip` or `conda`.

2) Create a new notebook by creating a new `.ipynb` file. This can be done by either
    a) Using the command `touch <notebook name>.ipynb` in bash
    b) Using the command palette <kbd>CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>P</kbd> in VS Code.

3) Open the notebook. There will be an option **select kernel** in the top right corner. A new user might have to install the necessary `Python` + `Jupyter` extensions for VS Code. Once the extensions are installed, the **select kernel** menu will yield options to either:
    a) **Python Environments**: this will use an iPython kernel installed in the various environments across your projects. Back in step 1, we installed the `jupyter` package into our current environment, so an iPython kernel will be installed in our current environment which we may now use to run the notebook.

    b) **Jupyter Kernels**: this will search for interpreters / kernels of all programming languages we have installed on our local machine. For example, if we have Java, R, and Python installed, than these languages will appear under this option.

    c) **Existing Jupyter Server**: if you have a jupyter server already booted up (e.g. by running the command `jupyter lab` in bash), we can connect to that server using this option.

More documentation can be found here: <a href="https://code.visualstudio.com/docs/datascience/jupyter-notebooks">Working with Jupyter Notebooks</a>.

<br>

## Connecting To Databricks

Spark uses distributed compute to achieve high computational speeds on so-called "big data" sets. "Distributed compute" refers to the use of a **cluster** (a network of multiple computers). To properly leverage the speed of Spark, we must connect to cluster and run our code on a cluster. The easiest option is to use Databricks.

To connect VS Code to databricks, follow this guide: <a href="https://docs.databricks.com/en/dev-tools/vscode-ext/tutorial.html">VSCode Extension for Databricks</a>. NOTE: connecting VSCode to Databricks will require an OAuth (user to machine) authorization token; these tokens are not supported on the Databricks Community Edition, so users of the community edition will not be able to connect to their Databricks cluster through their local machines.

Consequently, users of the Databricks Community Edition will either have to upload the notebooks and data sources to their Databricks workspace and run the code there. Alternatively, the code can still be run on a local machine (we just lose the speed benefits of Spark).


<br>

---

<br>

# Data Sets and Materials

In order to do data science and machine learning, we need data sets to work on. Currently, the notebooks in the `notebooks` and `projects` section rely data sets provided in <a href="https://www.udemy.com/share/1013kq3@nLui0kwvGiCXm2CdzV9T21ZMNdVdkUDWdB9R2734wlR7yUpAVsodsMFJk-KJJVRxXA==/">Jose Portilla's PySpark course on Udemy</a>. This is a great course with fantastic lecture notes including an overview of how distributed computing, how to setup a Spark cluster compute, and general python basics. This notes in this repo focus primarily on the second half of the course regarding Spark dataframe operations and the MLlib library.

In order to run the notebooks in this repo, you will need to a `course_materials` folder in project's root folder. It is generally good practice to not store data on a github repo, so the `.gitignore` file has been setup to prevent git from tracking the `course_materials` folder.

The user may also wish to play around with their own data sets. It is recommended that the user creates a `data` folder in project's root folder and store their own data sets there.The `.gitignore` file has been setup to prevent tracking on the `data` folder as well. Future efforts will be made to migrate notebooks and notes to use publically available data sources from <a href="kaggle.com">Kaggle</a>, <a href="https://archive.ics.uci.edu/">The UC Irvine ML Repository</a>, and other potential sources. These data sets will be stored in the `data` folder.


<br>

---

<br>
