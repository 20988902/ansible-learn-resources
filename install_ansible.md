
#安裝 ansible

##requirements
control 端 （python > 2.6,2.7)
managed 端 （python > 2.5)

## install via

###pip

`pip install ansible`

沒有pip 裝
```
wget https://bootstrap.pypa.io/ez_setup.py -O - | python
easy_install pip
```

或者沒有python > 2.7 先裝pyenvs (越搞越大？）
```
git clone https://github.com/yyuu/pyenv.git ~/.pyenv
git clone https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv

#add .bashrc
echo 'export PATH="$HOME/.pyenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

source ~/.bashrc

#pyenv require library

sudo apt-get install -y python-dev libffi-dev libssl-dev libxml2-dev libxslt1-dev
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev python3-dev
```


###yum redhat/centos

 `sudo yum install ansible`

###apt  
//官方建議作法
```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

### osx

1.pip way (同上)  
2.brew way `brew install ansible`
