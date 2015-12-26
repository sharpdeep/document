# Python pdb调试

python中有个pdb模块，使python代码也可以像gdb那样进行调试，一般情况下pdb模块可以在代码内直接使用，也可以通过命令行参数的形式添加该模块进行调试(`python -m pdb file.py`)。在代码中直接使用pdb模块调试时，import pdb模块后，然后在需要调试的代码出添加`pdb.set_trace()`命令即可，运行程序后，在运行到此代码处会自动停止，进入调试模式。

一般常用的调试命令有如下：
```
q  退出debug
h  打印可用的调试命令
b  设置断点，b 5 在第五行设置断点
h command  打印command的命令含义
disable codenum  使某一行断点失效
enable codenum   使某一行的断点有效
condition codenum xxx  针对断点设置条件
c    继续执行程序，直到下一个断点
n    执行下一行代码，如果当前语句有函数调用，则不会进入函数体中
s    执行下一行代码，但是s会进入函数
w    打印当前执行点的位置
j    codenum  让程序跳转到指定的行
l    列出附近的源码
p    打印一个参数的值
a    打印当前函数及参数的值
回车  重复执行上一行
```
测试代码如下sum.py：
```python
#/usr/bin/python
 
def add_t( ):
    i=1
    sum=0
    for i in range(1,5):
        sum=sum+i
        print sum
if __name__ == '__main__':
    add_t()
```
调试过程如下：`python -m pdb sum.py`

n调试
```
 > /opt/sum.py(3)<module>()
-> def add_t( ):
(Pdb) n
 > /opt/sum.py(9)<module>()
-> if __name__ == '__main__':
(Pdb) n
 > /opt/sum.py(10)<module>()
-> add_t()
(Pdb) n
1
3
6
10
--Return--
 > /opt/sum.py(10)<module>()->None
-> add_t()
(Pdb) q
```

n表示执行下一行代码，但是不陷入函数内部，可以看第3、6、9行，在执行add_t函数时并未陷入函数内部。

s调试
```
 > /opt/sum.py(3)<module>()
-> def add_t( ):
(Pdb) s
 > /opt/sum.py(9)<module>()
-> if __name__ == '__main__':
(Pdb) s
 > /opt/sum.py(10)<module>()
-> add_t()
(Pdb) s
--Call--
 > /opt/sum.py(3)add_t()
-> def add_t( ):
(Pdb) s
 > /opt/sum.py(4)add_t()
-> i=1
(Pdb) s
 > /opt/sum.py(5)add_t()
-> sum=0
(Pdb) s
 > /opt/sum.py(6)add_t()
-> for i in range(1,5):
(Pdb) s
 > /opt/sum.py(7)add_t()
-> sum=sum+i
(Pdb) s
 > /opt/sum.py(8)add_t()
-> print sum
(Pdb) p i
1
(Pdb) p sum
1
(Pdb) s
1
 > /opt/sum.py(6)add_t()
-> for i in range(1,5):
(Pdb) s
 > /opt/sum.py(7)add_t()
-> sum=sum+i
(Pdb) s
 > /opt/sum.py(8)add_t()
-> print sum
(Pdb) p i
2
(Pdb) p sum
3
(Pdb)
```

s调试和n调试一样，只不过s在遇到函数时会进入函数进行调试，9、12、13表示进入add_t函数内部进行调试，后面使用p命令打印相关函数内参数的值，后面输入r即可退出函数内部的调试。



