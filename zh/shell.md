## shell脚本学习笔记

### shell数组

在Bash中,数组变量有两种赋值方式:
 + name=(value1 ... valuen)
 + name[index]=value
数组的下标是从0开始的.

1.shell数组所有元素为 ${array[*]}
2.shell数组元素个数为 ${#array[@]} 或者 ${#array[*]}
3.字符串的长度 ${#str}

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

