# linux操作系统

## ssh和免密登录

### ssh

```
ssh -o ServerAliveInterval=60 root@106.13.85.199
```

### ssh-keygen

### MAC安装ssh-copy-id

```sh
git clone https://github.com/beautifulcode/ssh-copy-id-for-OSX
cd ssh-copy-id-for-OSX
chmod +x install.sh
./install.sh
```

### ssh-copy-id

```sh
ssh-copy-id root@106.13.85.199
```

### man

```
man ssh
```

## vim

### vim四种模式

普通模式

命令模式

插入模式 I,i,A,a,O,o

可视模式

```sh
:q
:q!
:w
:wq
:wq!
```

### vim命令

| 操作        | 命令                       |
| ----------- | -------------------------- |
| 删除        | x d dd ndd dw d$ d^ dG dnG |
| 复制        | y yy yG ynG y$ y^          |
| 粘贴        | P p                        |
| 移动光标    | gg GG ngg                  |
| 替换        | R cc cG cnG c$ c^          |
| 可视块 还原 | ctrl + v u                 |

```sh
:set number
:set nu
:split +文件名切分窗口
```

搜索

```
/ +内容
n向下查找
N向上查找
```



### vim官方教程

```sh
vimtutor
```

ctrl+z挂起

bg查询后台

fg将后台切换到前台

### vimrc

~/.vimrc

## github

```sh
sudo vim /etc/hosts
```

sudo apt install git

## linux发展史

1.出现：linus。

Minix系统，教授讲课。

2.Unix

Multics->Unics->Unix



BSD->netbsd

​          openbsd

Sun

Unix->linux

Unix->mac

redhat



linux -> debian -> Ubuntu

​						    -> deepin

​         -> Fedora -> RHEL -> centos

​	    -> Suse Opensuse

### windows

dos系统-》IBM

给苹果

windows3.0

excel、word。。。

win vista

win7....win10

### 苹果系统

macos

imac,ipod,iphone

## SHELL

### shell,teminal,console

shell:命令解释器

console：输出

terminal

### teminal

display(stdout,stderr)

keyboard(stdin)

### bash

terminal->shell->bash\zh\sh

### 全局设置和个人设置

系统启动之后，全局设置

登录到某个用户，该用户的个人设置

#### 全局设置

```sh
/etc/bash.bashrc
/etc/bash.profile
/etc/bash.bash.logout
```

#### 个人设置

```sh
~/.bashrc
~/.bash_profile
~/.bash_logout
~/.input
```

### shell编程

```sh
#!/bin/bash
echo 'hello world'
```

#### 变量和局部变量

```sh
a = 123
a = helloworld
a = `ssh_tmp`
```

```sh
local a = 12
```

#### 特殊变量

```sh
$0 当前shell脚本的名字，文件名
$n 脚本的第n个参数
$* 把所有参数视为字符串
$# 获取脚本参数个数
$@ 获取程序所有参数，有空白"$1" "$2"...
$? 判断上一条命令是否成功执行(成功为0)
$$ 获取当前进程pid
$! 上一条命令的pid
```

#### 变量、参数展开

```sh
${parameter:-word} 如果变量未被定义，表达式为word的值
${parameter:=word} 如果变量未被定义，设置变量为word的值，返回表达式为word的值
${parameter:?word} 捕捉由于变量未被定义而导致的错误退出程序
${parameter:+word} 如果parameter不为null或者未设置，则整个参数替换表达式值为word
${#parameter}输出长度
${parameter:offset}从offset截取字符串
${parameter:offset:length}从offset截取length字符串
${parameter/pattern/string}找到第一个替换
${parameter//pattern/string}找到所有替换
${parameter/#pattern/string}以pattern字符串开头的变量进行替换
${parameter/%pattern/string}以pattern字符串结尾替换
${parameter,,}全部小写
${parameter^^}全部大写
${parameter,}首字母小写
${parameter^}首字母大写
```

#### 输入输出

```
read
-a 数组 
-d 字符     以字符为输入的结束
-e 使用命令行方式读入
-n num num个字符读入
-p 提示信息
-r 不转义字符
-s silent模式
-t sec 设定超时间
-u fd 文件描述符读入
```

```sh
echo 字符串
-e开启转义
```

#### 函数

```sh
function test1 {
	echo "test1"
	return
}
test2() {
	echo "test2"
	return
}
function test3() {
	echo "test3"
	return
}
```

#### 流程控制

```sh
if [[ condition ]]; then
	#...
fi

if [[ condition ]]; then
	#...
	else
		#...
fi

if [[ condition ]]; then
	#...
elif [[ condition ]]; then
	#...
elif [[ condition ]]; then
	#...
	else
		#...
fi
```

```sh
while [[ condition ]]; do
	#...
done

for (( i = 0; i < 10; i++ )); do
	#...
done
```

```sh
until [[ condition ]]; do
	#...
done
```

```sh
case word in 
	pattern ) 
	;;
esac
```

#### 数组

```sh
declare -a b
b[100]=123
b=(1 2 3 4)

${b[*]}
${b[@]}

${#b[@]}

```

#### shell素数筛

```sh
declare -a prime
Start=$1
End=$2
for (( i=2; i < ${End}; i++));do
        if [[ ${prime[$i]}x == x ]];then
                prime[0]=$[ ${prime[0]} + 1 ]
                prime[${prime[0]}]=$i
        fi
        for (( j=1; j<=${prime[0]}; j++));do
                if [[ $[ $i * ${prime[$j]} ] -gt $End ]];then
                        break
                fi
                prime[ $[ $i * ${prime[$j]} ] ]=1
                if [[ $[ $i % ${prime[$j]} ] -eq 0 ]];then
                        break
                fi
        done
done

for (( i=1; i <= ${prime[0]}; i++));do
        if [[ ${prime[$i]} -lt $Start ]];then
                continue
        fi
        echo ${prime[$i]}
done

```