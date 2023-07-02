## Reference

+ 官方文档 https://docs.python.org/3/

+ Python Cookbook 中文 http://python3-cookbook.readthedocs.io/zh_CN/latest/

+ https://automatetheboringstuff.com/

  "In automate the Boring Stuff with Python, you'll learn how to use Python to write programs that do in minutes what would take you hours to do by hand-no prior programming experience required."



## Install (Ubuntu)

Normally python is installed. Check version:

```shell
python3 --version
python --version
```



Install pip for Python 3:

```shell
sudo apt install python3-venv python3-pip
# check version
pip3 --version
```



Update

After installed python and pip, this one can ensure pip, setuptools and wheel are up to date.

```python -m pip install --upgrade pip setuptools wheel```



## Virtual Environments

#### Creating Virtual Environments

```shell
# This will create the tutorial-env directory if it doesn't exist, and also create directories inside it containing a copy of the Python interpreter, the standard library, and various supporting files.
python3 -m venv tutorial-env

# Activate it
# Unix or MacOS
source tutorial-env/bin/activate

# Windows
tutorial-env\Scripts\activate.bat
```

http://www.runoob.com/java/java-tutorial.html