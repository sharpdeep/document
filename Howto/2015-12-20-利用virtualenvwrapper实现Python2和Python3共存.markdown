# 利用virtualenvwrapper实现Python2和Python3共存

关于virtualenvwrapper可以查看以下文档了解：
[Virtualenvwrapper Docs](http://virtualenvwrapper.readthedocs.org/en/latest/)
[virtualenvwrapper多环境管理扩展](http://www.nowamagic.net/academy/detail/1330231)

virtualenvwrapper在平时的应用中主要用于**为每个项目建立一个独立的虚拟环境，**让每个项目的依赖模块不共享，使得不同版本的模块可以同时存在。

除此之外，在建立virtualenvwrapper虚拟环境的时候也可以指定环境的python版本，也就是说在同一台机器上，一个项目用着python2，一个项目用着python是可行的。

详细操作如下：

###1. 安装virtualenv, virtualenvwrapper
```
$ sudo pip install virtualenv
$ sudo pip install virtualenvwrapper
```
如果还没有安装pip的话先安装pip
```
$ sudo apt-get install python-pip python-dev build-essential 
$ sudo pip install --upgrade pip
```
###2. 安装python3.x(ubuntu自带python2.7)
apt-get安装
```
$ sudo apt-get install python3.4
```

###3. 创建环境
创建python2.x环境
```
mkvirtualenv env27
```
创建python3.x环境
```
mkvirtualenv -p python3.4目录/bin/python3.4 env34
```
apt安装的python3.4目录一般是在`/usr/local/lib/python3.4`下。

如果没有指定，默认情况下是python2.x。

###4. 切换
```
$ workon env27
```
看一下python的版本
```
$ python --version
```
> Python 2.7.6

再切到3.4的环境
```
$ workon env34
```
查一下版本
```
$ python --version
```
> Python 3.4.0

看来两个版本的python都工作正常：）

###5. 退出环境：
```
$ deactivate
```

###6. 删除环境： 
```
$ rmvirtualenv env_name
```



