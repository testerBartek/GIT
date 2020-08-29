# Python 3.X



## Python 3

### install python

{% embed url="https://www.python.org/" caption="Just download and install from main website of python." %}

### Set environment Variables

1. open "environment Variables"
2. set at System Variables New variable "PYTHONPATH"
3. Add paths like on first screen
4. Create on Variable Path \(System variables\) a new variable named %PYTHONPATH%
5. The Paths of PYTHONPATH will be use in Path by %PYTHONPATH%

![Add paths to python](.gitbook/assets/image%20%2869%29.png)

![%PYTHONPATH%](.gitbook/assets/image%20%2812%29.png)

At command prompt / powershell just try command to check if python is correctly installed

`python -V  
>Python 3.8.5`

## Pycharm \(IDE\)

### Install Pycharm

{% embed url="https://www.jetbrains.com/pycharm/" %}

Download and install Pycharm Community version - it is for free.

### Create first project

File &gt; New Project  
1. set a location and new folder name  
2. set a New environment \(it's better option, because sometimes we forgot to tell someone what to install in his environment to this project could be work\)

![Create a new project with new environment on Python 3.8](.gitbook/assets/image%20%289%29.png)

### Install pip to Python Interpreter

1. File &gt; Settings 
2. Project: "gitbookProject" &gt; Python Interpreter 
3. Click "+" icon &gt; to install

![to install package](.gitbook/assets/image%20%2844%29.png)

4. search and install package

![Install selenium package](.gitbook/assets/image%20%282%29.png)

5. Package 'selenium' installed successfully

## Pip and Venv by console

{% embed url="https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/" %}

### Package manager

pip is the reference Python package manager. It’s used to install and update packages. You’ll need to make sure you have the latest version of pip installed.

```text
py -m pip install --upgrade pip
```

### Virtual environment

Virtual environment is used to manage Python packages for different projects. Using virtualenv allows you to avoid installing Python packages globally which could break system tools or other projects. You can install virtualenv using pip.

#### Creating a venv

```text
py -m venv env
```

\(we could do it by pycharm by option New environment\)

#### Activating a virtual environment

```text
.\venv\Scripts\activate
```

#### Leaving a virtual environment

```text
deactivate
```

#### Pip install

e.g. selenium

```text
pip install selenium
```

### How to use venv and pip

![](.gitbook/assets/image%20%2846%29.png)





