# python 安装

## 安装python环境
> 参考: [Linux下安装python 2.7](https://www.jianshu.com/p/6425d18d3e47)

```
yum -y install wget python-devel openssl openssl-devel gcc gcc-c++ zlib* sqlite sqlite-devel mysql-devel libxml2-devel libxslt-devel

cd ~
wget https://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz
tar -zxvf Python-2.7.14.tgz
cd Python-2.7.14

yum install  
./configure && make && make altinstall

# 备份旧python相关命令
mv /usr/bin/pip /usr/bin/pip_old
mv /usr/bin/easy_install /usr/bin/easy_install_old
mv /usr/bin/python /usr/bin/python_old

# 新版本python命令做软连接，快捷使用
ln -s /usr/local/python2.7/lib/libpython2.7.so /usr/lib
ln -s /usr/local/python2.7/lib/libpython2.7.so.1.0 /usr/lib
ln -s /usr/local/python2.7/bin/python2.7 /usr/bin/python
ln -s /usr/local/python2.7/lib/libpython2.7.so /usr/lib64
ln -s /usr/local/python2.7/lib/libpython2.7.so.1.0 /usr/lib64


# 安装pip
cd ~
wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py
# 软链接
ln -s /usr/local/bin/pip /usr/lib/pip


# 安装easy_install
cd ~
wget https://bootstrap.pypa.io/ez_setup.py
python ez_setup.py 
# 软链接
ln -s /usr/local/bin/easy_install /usr/bin/easy_install
```

## 安装python虚拟环境
```
pip install virtualenv
pip install virtualenvwrapper
ln -s /usr/local/bin/virtualenv /usr/bin/virtualenv
# 设置虚拟环境home目录
export WORKON_HOME=~/.virtualenvs
# 启动虚拟环境加入到环境变量
vim ~/.bashrc
> export WORKON_HOME=$HOME/.virtualenvs
> export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python
> export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
> source /usr/local/bin/virtualenvwrapper.sh
```

