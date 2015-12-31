#Ubuntu下JDK多版本共存与切换

Android L之后推荐使用JDK7编译程序，这是自然发展规律，就像是4年前编译Android 1.6需要使用JDK5一样。

多版本JDK是可以共存的，只需要使用**update-alternatives**工具就可以随时将它们切换。下面描述安装openjdk和oracle jdk（对不住了sun）以及切换版本的过程。

##一、安装openjdk7

```
$ sudo apt-get update  
$ sudo apt-get install openjdk-7-jdk  
```

安装完成后找到其安装路径：

```
$ dpkg -L openjdk-7-jdk  
/.  
/usr  
/usr/lib  
/usr/lib/jvm  
/usr/lib/jvm/java-7-openjdk-amd64  
```
```
$ ls /usr/lib/jvm/java-7-openjdk-amd64/  
ASSEMBLY_EXCEPTION  bin  docs  include  jre  lib  man  src.zip  THIRD_PARTY_README  
```

##二、切换java版本

```
$ sudo update-alternatives --config java  
There are 2 choices for the alternative java (providing /usr/bin/java).  

  Selection    Path                                            Priority   Status  
------------------------------------------------------------  
* 0            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      auto mode  
  1            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      manual mode  
  2            /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java   1051      manual mode  
  
Press enter to keep the current choice[*], or type selection number: 2  
update-alternatives: using /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java to provide /usr/bin/java (java) in manual mode.  

``` 


```
$ java -version  
java version "1.7.0_65"  
OpenJDK Runtime Environment (IcedTea 2.5.3) (7u71-2.5.3-0ubuntu0.12.04.1)
```

##三、安装Oracle jdk

使用Android Studio做开发，启动IDE就提示：

> OpenJDK shows intermittent performance and UI issues. We recommend
> using the Oracle JRE/JDK.

看来还是要安装Oracle的JDK了，因为ubuntu软件源中没有此JDK，所以不能像安装openjdk一样使用apt-get工具。
那么我们还是要去[官网下载jdk7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)。

按照以往的惯例，我将这些软件放在`/opt`目录下。将JDK解压到新建目录jdk下。
用update-alternatives工具来添加java可选配置项（这是一个dpkg的一个实用工具）。

```
$ sudo update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.7.0_71/bin/java 700  
$ sudo update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.7.0_71/bin/javac 700  
$ sudo update-alternatives --install /usr/bin/jar jar /opt/jdk/jdk1.7.0_71/bin/jar 700  
```

700是优先级数值，我这里随便使用了一个数。
查看一下我们的config：

```
$ sudo update-alternatives --config java  
There are 3 choices for the alternative java (providing /usr/bin/java).  
  
  Selection    Path                                            Priority   Status  
------------------------------------------------------------  
  0            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      auto mode  
  1            /opt/jdk/jdk1.7.0_71/bin/java                    700       manual mode  
  2            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      manual mode  
* 3            /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java   1051      manual mode  
  
Press enter to keep the current choice[*], or type selection number: 1  
update-alternatives: using /opt/jdk/jdk1.7.0_71/bin/java to provide /usr/bin/java (java) in manual mode  
```

验证是否切换成功：

```
$ java -version  
java version "1.7.0_71"  
Java(TM) SE Runtime Environment (build 1.7.0_71-b14)  
Java HotSpot(TM) 64-Bit Server VM (build 24.71-b01, mixed mode)  
```

同样的，当我们需要切换到低版本时选择2或者安装oracle jdk6并将其纳入管理。这样就可以不用通过手动修改环境的方式来灵活切换JDK的版本了。