# first
llvm主要分为前端，后端和中间优化IR
在词法分析方面中，词法分析器有三种设计方法
1、antlr词法分析器生成器
grammar SimpleExpr;

plog : star* EOF ;

star : expr ';'
     | expr '=' expr ';'
     | 'print' expr ';';

expr :  expr ('*' | '/') expr
        |expr ('+' | '-') expr
        |'(' expr ')'
        |ZIMU
        |INT
        |FLOAT
        ;


ZIMU : ('_'|[a-zA-Z]) ('_'|[a-zA-Z0-9])*;
KONGGE : [ \r\t\n]+ -> skip;
INT : '0' | ('+'|'-')? [1-9]SHUZI*;
FLOAT : SHUZI* '.' SHUZI+;
ZHUSHI : '//' .*? '\n' -> skip;
WENJIANZHUSHI : '/**' .*? '*/' -> skip;
DUOHANGZHUSHI : '/*' .*? '*/' -> skip;
SHUZI : [0-9];

2、手写词法分析器
3、自动化词法分析器
通过正则表达式RE到词法分析器的生成：（1）RE通过汤姆森构造法生成NFA（2）NFA通过子集构造法生成DFA（3）DAF最小化最后生成词法分析器的代码

定义两个状态的等价关系，只要通过同种字符到达的状态是等价的，那么这两个状态就是等价的
可以先判断接收状态是不是等价的，如果接收状态等价可以一步步往前推判断两个状态是否是等价的

正则表达式中：
\bcat\b
\b    \b单词边界
匹配单词cat而不是某个单词的cat字母部分

^    $为字符串边界，以字符串开头，以字符串结尾，但多行表示为一个字符串，不是自己想要的则开启多行模式可以一行表示一个字符串

反向引用
后面1-6中的数字匹配需与前面的数字相同
<[hH]([1-6])>.*?<\/[hH]\1>

linux 操作系统系统ls命令的作用

1、ls命令的参数的作用：

可以指定要查看的文件夹（目录）的内容，如果不给定参数，就查看当前工作的目录的内容（默认home目录）

2、ls命令的选项:
ls -a展示全部的目录
ls -l 以列的形式将目录展示出来
ls -h必须与-l组合使用（比如：ls -lh）表示以易于阅读的形式列出来，（给出内存的单位kb，mb，gb等等）

3、ls命令选项的组合使用：
语法中的选项可以组合使用比如说 -a和-l可以一起使用
表示：以列的形式把所有的内容全部展示出来。有三种写法都可以
比如ls -al
       ls -la
       ls -a -l
注意空格


4、CD切换工作目录：
cd命令（change directory）切换当前所在工作目录
比如输入cd / 表明要切换到根目录，cd /boot 切换到跟目录下的boot目录中，以此类推

5、pwd（Print Work Directory）命令用来查看当前所在的工作目录，直接输入pwd即可


6、相对路径和绝对路径
当前目录/home/q下ls查看，目录下有一个Music目录，我们需要切换到Music目录
绝对路径：cd /home/q/Music
相对路径：cd Music
总结：绝对路径是以根目录开头，描述路径的一种写法，路径描述以/开头
          相对路径是以当前目录开头，描述路径的一种写法，路径描述无需以/开头

7、特殊路径符：
.表示当前目录，比如cd ./Desktop表示切换到当前目录下的Desktop目录内，和cd Desktop效果一致
..表示上一级目录，比如：cd ..即可切换到上一级目录，cd ../..表示切换到上二级目录，cd ../../..切换到上三级目录
~表示HOME目录，比如cd ~可切换到HOME目录，或cd ~/Music，切换到HOME目录内的Music目录

8、创建目录：make directory的缩写mksir
比如	当前在/home/q/Music目录下，我可以直接mkdir 目录名zhang表示在Music目录下创建了一个名为zhang的目录
注意：
mkdir -p zhi/shi/dr
中间加上-p的作用是可以一次性创建多个层级的目录


9、关于文件操作的命令part1
（1）touch +文件名（即Linux路径），表示创建文件，其中需要区别文件并不是文件夹目录，仅仅是一个文件
（2）cat +文件名（即Linux路径），表示查看文件，被查看的文件路径里，相对绝对特殊路径符都可以使用
（3）more +Linux路径同样表示查看文件，被查看的文件路径里，相对绝对特殊路径符都可以使用
注意：cat 与more不同的是，cat直接将内容直接显示出来；more 支持翻页，如果文件内容过多，可以一页页的展示
空格翻页，b上一页，q退出查看
扩展：more 是基础分页查看器，而 less 是高级分页查看器，可以自己试试，less更方便点

太多了就Ctrl +l清屏

10、文件操作命令part2


11、、cp可以用来复制文件以及文件夹
（1）cp 复制文件
cp test.txt1 test.txt2  意思是将文件test.txt1复制到2中，1是被复制的，完成之后2文件的内容就变得和1一样了
（2）cp 复制文件夹
cp -r 文件夹1 文件夹2 意思是将文件夹1复制到文件夹2，一定要加-r

12、mv(move)可以用来移动文件或者文件夹
mv 参数一 参数二
参数一，Linux路径，表示被移动的文件或者文件夹
参数二 ，Linux路径，表示要移动去的地方，如果目标不存在则进行改名，确保目标存在


13、rm（remove)命令常用来删除文件/文件夹 rm 参数一 参数二 参数三可以一次删除很多文件，中间用空格隔开
rm 文件名（用来删除当前工作目录中的文件）
rm -r 文件夹名（用来删除当前工作目录下的文件夹也就是目录）
rm -f（force)指强制删除（不会弹出提示确认信息，普通用户删除内容不会弹出信息，只有管理员root 用户删除内容有提示，所以一般普通用户用不到-f选项）

注：rm命令支持通配符 rm  *s 表示删除当前工作目录中所有以s结尾的文件
test*，表示匹配任何以test开头的内容
*test，表示匹配任何以test结尾的内容
*test*，表示匹配任何带有test的内容

rm是一个危险的命令，特别是处于root 用户的时候，一定要谨慎使用。（使用超级用户权限指令 su - root，退回普通用户用exit）


14、whichi 要查找的命令
其实cd pwd 等命令的本体都是一个个的二进制执行程序，可以找到所使用的一系列的命令文件放在哪里
比如我想找找cd 这个程序执行的文件在哪里我就可以直接 which cd
同理可得which pwd /which rm/which cat 等等

15、
（1）
find命令-按文件名查找文件
find 起始路径-name 文件目录名
起始路径：表示从哪开始找，也可以不加表示从当前工作目录中查找）
-name表示按文件名查找
注意也可以匹配通配符，find / -name "*zmq*"表示从根目录中查找名字里包含zmq的文件
（2）
find -size [+/-]10[kMG]（大小写严格遵守）
-size 表示按文件大小来查找文件
+/-表示大于和小于多大内存的
10随意表示的一个数字，可以换成任何其他的自然数
k表示kb，M表示MB，G表示GB。



16、grep命令
grep 过滤文件中的带有关键字的行 grep [-n] “关键字” itheima（文件路径）
意思是输出文件itheima中带有关键字标识符的行，-n可写可不写，写了还会输出行数表示过滤的第几行
比如说文件itheima的内容为
i am a bad girl~
hello everyone.
下面演示
[q@localhost ~]$ grep "girl" itheima
i am a bad girl~

 grep "l" itheima
i am a bad girl~
hello everyone.
[q@localhost ~]$ grep -n "l" itheima
1:i am a bad girl~
2:hello everyone.


17、wc命令
wc命令做数量统计wc [-c -m -l -w] 文件路径
-l，统计行数
-w，统计单词数量
-c，统计字节数--bytes数量
-m，统计字符数量
注意，统计单词数量实际上用空格分开的两边数量比如iyy hio这就是两个单词，iyyhiocat就是一个单词
假如我们什么都不加直接wc 文件名，比如itheima文件
 wc itheima
结果： 2  7 33 itheima
什么都不加，默认统计文件内容数量：2为行数，7为单词数，33为bytes数量（可以用-lh来验证）



18、管道符的使用 |（shift+enter上面那个键)
管道符可以让左边命令的输出作为右边命令的输入。意思是左边的结果作为右边的输入，管道符可以嵌套使用。
比如有一个ds文件内容为llo 还有一个itheima文件内容为
i am a bad girl~
hello everyone.
单独cat ds时，查看ds文件的内容，输出结果为llo
单独wc -l时，意思是查看某文件路径的行数，但不给文件，当然这个文件的输入可以通过管道符前面的命令输入进来
 cat ds | wc -l
输出结果：1
因为llo只有一行，所以wc -l 的结果为1
例
统计文件itheima中带有l关键字的有几行
cat itheima | grep "l" | wc -l
输出结果：2
例：
 ls -l
总用量 12
drwxrwxr-x. 2 q q  6 8月  27 02:30 d
drwxrwxr-x. 2 q q  6 8月  27 02:31 ddd
drwxr-xr-x. 2 q q  6 8月  11 02:34 Desktop
drwxr-xr-x. 2 q q  6 8月  11 02:34 Documents
drwxr-xr-x. 2 q q  6 8月  11 02:34 Downloads
-rw-rw-r--. 1 q q  4 8月  27 03:35 ds
drwxrwxr-x. 2 q q  6 8月  27 02:31 e
drwxrwxr-x. 3 q q 21 8月  11 20:50 itcast
-rw-rw-r--. 1 q q 33 8月  27 02:53 itheima
drwxrwxr-x. 2 q q  6 8月  27 02:31 l
drwxr-xr-x. 4 q q 37 8月  26 04:10 Music
drwxrwxr-x. 2 q q  6 8月  27 02:31 n
drwxr-xr-x. 2 q q  6 8月  11 02:34 Pictures
drwxr-xr-x. 2 q q  6 8月  11 02:34 Public
drwxrwxr-x. 2 q q  6 8月  27 03:27 q
drwxr-xr-x. 2 q q  6 8月  11 02:34 Templates
-rw-rw-r--. 1 q q 15 8月  27 03:13 test.txt
drwxr-xr-x. 2 q q  6 8月  26 03:55 Videos
drwxrwxr-x. 3 q q 15 8月  27 02:36 y
drwxrwxr-x. 5 q q 37 8月  27 02:32 zmq
[q@localhost ~]$ ls -l | wc -l
21

19、
echo输出命令，带有空格或特殊符号时，最好使用双引号
echo 123456
结果：123456
echo “我喜欢美丽的自然风景”
结果：我喜欢美丽的自然风景

反引号`
反引号包围的内容会被当成命令执行而不是普通字符
例：
[q@localhost ~]$ echo pwd
pwd
但其实我们想要这个pwd的结果[q@localhost ~]$ pwd
/home/q
就可以加上两个反引号包围
[q@localhost ~]$ echo `pwd`
/home/q

例：
[q@localhost ~]$ echo `cat itheima`
i am a bad girl~ hello everyone.


20、重定向符
>，将左侧命令的结果覆盖到右边的文件中
例如echo "hello" > itheima，结果就是itheima文件的内容变为hello，ls -l > itheima也一样
>>，将左侧命令的结果追加到右边的文件中
例如echo "世界很美丽" >> itheima，结果就是itheima文件的之前内容不变，后面加上一句世界很美丽

21、tail命令，tail[-f -num] 文件路径，可以查看文件尾部内容，跟踪文件的最新更改
-num ,表示尾部查看多少行，不填默认10行
-f表示持续追踪当不写-num的时候，默认先追踪十行，Ctrl+c退出追踪
