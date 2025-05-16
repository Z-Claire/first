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
