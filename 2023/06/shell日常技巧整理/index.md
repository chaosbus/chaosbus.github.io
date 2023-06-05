# Shell日常使用技巧整理


## 文本处理

```sh
var=appletcat

# 从x位开始的n个字节
echo ${var:3:2}

# 长度
echo ${#var}

# 变量保护
dir1="/home"
dir2=
echo "path1 : ${dir}/${dir2}"
echo "path2 : ${dir}/${dir2:?"dir2_is_null"}"
```

## sed

```sh
sentence="He ate an apple before."

echo $sentence | sed 's/apple/banana/g'
echo $sentence | sed "s/apple/banana/g"

v=pear
# 使用变量必须使用：{}，并用双引号
echo $sentence | sed "s/apple/${v}/g"

# 使用多个匹配
echo $sentence | sed -e "s/apple/banana/g" -e "s/He/Dog/g"

# 保留关键字，使用()，\x
echo $sentence | sed  "s/He\s\(.*\) before./\1/g"

# 过滤文件中的空行：
sed -e '/^$/d'
```

## 前后缀

```sh
# 路径前缀后缀
path=/Users/Joe/nginx/conf
dirname $path
basename $path


# 获取文件名及后缀
ff=build.xml
# 前缀名
echo ${ff%.*}
# 后缀名
echo ${ff##*.}
```

## 用`${}`分别替换得到不同的值

> \#去掉左边（键盘上#在`$的左边）
> 
> %去掉右边（键盘上%在$`的右边）
> 
> 单一符号是最小匹配；两个符号是最大匹配

```sh
file=/dir1/dir2/dir3/my.file.txt

# 删掉第一个 / 及其左边的字符串：dir1/dir2/dir3/my.file.txt
echo ${file#*/}
# 删掉最后一个/及其左边的字符串：my.file.txt
echo ${file##*/}
# 删掉第一个 . 及其左边的字符串：file.txt
echo ${file#*.}
# 删掉最后一个 . 及其左边的字符串：txt
echo ${file##*.}
# 删掉最后一个 / 及其右边的字符串：/dir1/dir2/dir3
echo ${file%/*}
# 删掉第一个 / 及其右边的字符串：(空值)
echo ${file%%/*}
# 删掉最后一个 . 及其右边的字符串：/dir1/dir2/dir3/my.file
echo ${file%.*}
# 删掉第一个 . 及其右边的字符串：/dir1/dir2/dir3/my
echo ${file%%.*}
```

* 排序去重

```sh
# 按第2位排重
csv="apple|1482|count
banana|832|sum
test|97|if
good|832|over"

echo "$csv" | awk -F'|' '!row[$2]++'


# 按照指定列排重
# -t指定分隔符，-k指定列范围（如果从第1列起到第1列结束）
sort -t ',' -u -k 1,1 test.csv


# 排除第4列为空的行
cat test.csv | awk -F',' '{if($4!="") {print $0}}' 

```

## 时间

```sh
# 格式化输出
date +'%Y-%m-%d %H:%M:%S'

# 某时间
date -d "1 day ago"

# 1970秒
secs=`date +%s`
date -d "0:0:0 1970-01-01  ${secs}sec"
date -d "1970-01-01  ${secs}sec" +"%Y-%m-%d %H:%M:%S"
date -d "0:0:0 1970-01-01  ${secs}sec 123 mins ago UTC" +"%Y-%m-%d %H:%M:%S"
```

## 数组

```sh
ARRAY=(
a1
b2
c3
c4
)

for mod in ${ARRAY[@]}
do
    echo ${mod}
done
```

## 命令

```sh
# 执行命令获取返回的2种写法
echo `uname -a`
echo $(uname -a)


# 获取自身PID
echo $$


# 变量算术运算
i=10
echo $((i*3/5))


# 循环的2种写法
for((i=0;i<4;i++))
do
    echo "> $i"
done

i=0
while [ $i -lt 4 ]
do
    echo "+ $i"
    $((i+1))
done 

```

## 传参

| 变量   | 含义                                                  |
| ---- | --------------------------------------------------- |
| \$0  | 当前脚本的文件名                                            |
| \$n  | 传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是`$1，第二个参数是$`2。 |
| \$#  | 传递给脚本或函数的参数个数。                                      |
| \$\* | 传递给脚本或函数的所有参数。                                      |
| \$@  | 传递给脚本或函数的所有参数。被双引号(" ")包含时，与 \$\* 稍有不同，下面将会讲到。      |
| \$?  | 上个命令的退出状态，或函数的返回值。                                  |
| \$\$ | 当前Shell进程ID。对于 Shell 脚本，就是这些脚本所在的进程ID。              |

```sh
# 上一个命令的处理结果，0成功
$?
# 参数个数
$#
# 同上，具体参数
$1, $2, ...
```

## 注释

* 区块注释

```sh
echo "start"

:<<BLOCK
# comments
echo "not execute"
BLOCK

echo "done"
```

## 判断变量中是否包含某字符串

```sh
str="this is a string"  
[[ $str =~ "this" ]] && echo "$str contains this"   
[[ $str =~ "that" ]] || echo "$str does NOT contain that"  
```

## 两个文件的差集、并集

* a.txt

```txt
a
d
b
c
1
```

* b.txt

```txt
1
a
3
5
7
```

* 并集

```sh
sort -u a.txt b.txt
```

* 交集

```sh
grep -F -f a.txt b.txt | sort | uniq
```

* 差集
  * a-b

    ```shell
    grep -F -v -f b.txt a.txt | sort | uniq
    ```

  * b-a

    ```sh
    grep -F -v -f a.txt b.txt | sort | uniq
    ```

