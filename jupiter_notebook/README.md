# Installation

```
$ pacman -S python-pip
$ pip3 install notebook
$ jupiter notebook
``` 

# Create Venv

```
$ pip install --user ipykernel
$ python -m ipykernel install --user --name=myvenv
```
 > Note: You will find the venv under "New" in Jupyter Notebook

# Remove the venv when not needed 

```
$ jupyter kernelspec uninstall myenv
```
