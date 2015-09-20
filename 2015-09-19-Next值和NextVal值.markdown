###计算前缀 Next[i] 的值:

我们令 next[0] = -1 。从 next[1] 开始，每求一个字符的 next值，就看它前面是否有一个最长的"字符串"和从第一个字符开始的"字符串"相等(需要注意的是，这2个"字符串"不能是同一个"字符串")。如果一个都没有，这个字符的 next 值就是0；如果有，就看它有多长，这个字符的 next 值就是它的长度。

###计算修正后的 Nextval[i] 值:

我们令 nextval[0] = -1。从 nextval[1] 开始，如果某位(字符)与它 next 值指向的位(字符)相同，则该位的 nextval 值就是指向位的 nextval 值(nextval[i] = nextval[ next[i] ])；如果不同，则该位的 nextval 值就是它自己的 next 值(nextvalue[i] = next[i])。或者用以下代码表示为：
```
if src[i]==src[next[i]]
    nextval[i]=nextval[next[i]];
else
    nextval[i]=next[i];
```

###例子：
|  i  |  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|  s  |  a  |  b  |  c  |  a  |  b  |  c  |  a  |  a  |
|next | -1  |  0  |  0  |  0  |  1  |  2  |  3  |  4  |
|nextVal|-1 |  0  |  0  |  -1 |  0  |  0  |  -1 |  4  |



