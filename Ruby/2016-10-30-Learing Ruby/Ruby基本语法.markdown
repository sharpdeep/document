### Ruby交互环境irb

#### 双引号和单引号字符串

单引号处理少，转义字符不处理

```
irb(main):021:0> puts 'hello\nworld'
hello\nworld
=> nil
irb(main):023:0> puts "hello\nworld"
hello
world
=> nil
```

#### 字符串表达式内插 -- 适用于双引号字符串

```
irb(main):034:0> name = "sharpdeep"
=> "sharpdeep"
irb(main):035:0> puts "hello,#{name}"
hello,sharpdeep
=> nil
irb(main):036:0> puts "hello,#{-1942.abs}"
hello,1942
=> nil
```

全局变量、实例变量和类变量可以不需要花括号

```
irb(main):037:0> $greeting = "hello"
=> "hello"
irb(main):038:0> @name = "Bear"
=> "Bear"
irb(main):039:0> puts "#$greeting,#@name"
hello,Bear
=> nil
```

#### 若没有返回值，则方法最后一个表达式的值将会被返回

```
irb(main):041:0> def say_hello(name)
irb(main):042:1>   "hello,#{name}"
irb(main):043:1>   end
=> :say_hello
irb(main):044:0> puts say_hello("Bear")
hello,Bear
=> nil
```

#### 命名惯例

- 全局变量以`$`开头
- 实例变量以`@`开头
- 类变量以`@@`开头
- 类名称、模块名称、常量以大写字母开头
- 局部变量、方法名以小写字母或下划线开头
- `$`和`@`符号后不能接数字
- 方法名可以用`?`，`!`，`=`结束

#### 数组

- 索引是数字
- 可以存不同类型对象

数组字面量 -- 直接方括号

```
irb(main):052:0> a = [1,'dog',2,'cat']
=> [1, "dog", 2, "cat"]
irb(main):053:0> a[1]
=> "dog"
irb(main):054:0> a[4]  #不存在
=> nil
```

快速创建字符数组

```
irb(main):060:0> a = %w{cat dog bee} # 大括号，空格分割
=> ["cat", "dog", "bee"]
irb(main):061:0> a[1]
=> "dog"
```

#### 散列表

- 索引可以是任意对象
- 可以存储不同类型的对象
- key-value结构，key必须唯一

散列表字面量 -- 直接大括号

```
irb(main):069:0> inst_section = {
irb(main):070:1*     'cello' => 'string',
irb(main):071:1*     'clarinet' => 'woodwind',
irb(main):072:1*     'drum' => 'percussion'
irb(main):073:1>   }
=> {"cello"=>"string", "clarinet"=>"woodwind", "drum"=>"percussion"}
irb(main):074:0> inst_section['drum']
=> "percussion"
```

散列表key不存在时指定默认返回值

```
irb(main):080:0> h = Hash.new(0) # 新建空的散列表，并指定默认值为0
=> {}
irb(main):081:0> h['key1'] = 'value1'
=> "value1"
irb(main):082:0> h['key1']
=> "value1"
irb(main):083:0> h['key2']
=> 0
```

#### 条件结构

```
if count > 10
  puts "try again"
elsif count  == 3
  puts "you lose"
else
 puts "enter a number"
end
```

语句修饰符形式

```
puts "you are child" if age < 18
```

#### 循环结构

```
while line.gets
  line.downcase
end
```

语句修饰符形式

```
square = 2
square = square * square while square < 100
```

#### 正则表达式

**/正则表达式/**表示一个正则表达式

`=~`判断字符串是否符合正则表达式，如果匹配返回第一个匹配的位置，如果没匹配则返回nil

```
word = "Python"
if word =~ /Python|Ruby/
  puts "the language is #{word}"
end
```

`sub`函数替换第一个匹配的字符串
`gsub`函数替换所有匹配的字符串

```
word = "Python"
word.sub(/ython/,"erl") #word字符串并没有改变
```

#### block

定义：用花括号或do...end包起来的代码,约定俗成的是单行用花括号，多行用do...end
使用: 调用方法后
用途：调用方法中yield处调用block，用于实现迭代器

```
def call_block
  puts "start of the method"
  yield
  puts "end of the method"

call_block {puts "in the block"}
```
常用的each即是一个迭代器

```
animals = %w(dog cat bee)
animals.each(|animal| puts animal)
```

each 伪代码
```
def each
  for each or animals
    yield(animal)
  end
end
```

#### IO操作

常见的输出有3种：puts、print、printf

- puts：换行
- print 不换行
- printf 同C语言

输入：gets，从标准输入流
