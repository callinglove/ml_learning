## shell脚本学习笔记

### if语句

在shell编程中,大多数情况会用到测试命令来对条件进行测试.比如比较字符串、判断文件存在与否以及是否可读,通常用`[]`来.

> **注意:**`[``]`前后都需要空格,否则会引起语法错误.

if语句的格式如下:

```shell
if ... ; then
...
elif ...; then
...
else
...
fi
```

以下总结来自`man test`
 + **( EXPRESSION )**	表达式为真
 + **! EXPRESSION**		表达式为假
 + **EXPRESSION1 -a EXPRESSION2**	条件1与条件2都为真
 + **EXPRESSION1 -a EXPRESSION2**	条件1或条件为真
 + **-n STRING**		字符串的长度非零
 + **-z STRING**		字符串的长度为零
 + **STRING1 = STRING2**		字符串相等
 + **！=**		字符串不等
 + **-eq**		两者相等
 + **-ge**		>=
 + **-gt**		>
 + **-le**		<=
 + **-lt**		<
 + **-ne**		!=
 + **FILE1 -ef FILE2**	两个文件有相同的device和inode numbers
 + **-nt**		前者比后者新(修改时间)
 + **-ot**		older than
 + **-b FILE**	为块特殊文件
 + **-c FILE**	字符特殊文件
 + **-d FILE**	目录文件
 + **-e FILE**	文件存在
 + **-f FILE**	文件存在且为普通文件
 + **-x FILE**	文件可执行
 + **-w FILE**	文件可写
 + **-r FILE**	文件可读
 + **-s FILE**	文件存在且大小大于0
 + **-S FILE**	文件是socket

if语句应用实例:
```shell
#!/bin/sh
# 判断文件是否存在
YACCESS=`date -d yesterday +%Y%m%d`
FILE="access_$YACCESS.log.tgz"
if [ -f "$FILE" ]; then
	echo "OK"
else
	echo "error: no $FILE"
fi 
```

### for语句

### shell数组

在Bash中,数组变量有两种赋值方式:
 + name=(value1 ... valuen)
 + name[index]=value

数组的下标是从0开始的.

1. shell数组所有元素为 ${array[*]}
2. shell数组元素个数为 ${#array[@]} 或者 ${#array[*]}
3. 字符串的长度 ${#str}

编程实例:编写个shell脚本将当期目录下大于10K的文件名打印出来

```shell
#!/bin/bash
fileinfo=($(du ./*))
length=${#fileinfo[@]}
for((i=0;i<$length;i=$((i+2))));do
	if [ ${fileinfo[$i]} -gt 10 ];then
		echo ${fileinfo[$((i+1))]}
	fi
done
```
#### LaTex 公式
$$	x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$
