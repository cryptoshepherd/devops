# Python 3.9 on Ubuntu 20.04
> Procedure to install Python 3.9 as default
![](header.png)

## Download and Compile

```sh

sudo apt update

sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev

wget https://www.python.org/ftp/python/3.9.7/Python-3.9.7.tgz

tar zxvf Python-3.9.7.tgz

cd Python-3.9.7

./configure --enable-optimizations

make -j 12 ( check your Vcore with "nproc")

sudo make altinstall

```


## Install Pip for 3.9
```sh

wget https://bootstrap.pypa.io/get-pip.py -o get-pip.py

python3.9 get-pip.py

sudo nano ~/.bashrc

---
# Python / pip Alias
alias python='/usr/bin/python3.9'
alias pip='~/.local/bin/pip3.9'
---

source ~/.bashrc

```

## Install some Pre Req before use the new Python

```sh
sudo apt-get install python3.9-venv
```

## Create and Activate New Virtual Envs

python -m venv .venv

To activate (MacOSX and Linux):

source .venv/bin/activate

## Meta

Simone Arena – @the_lello – lellothegreat@protonmail.ch
