---
title: Shell学习积累
date: 2018-01-16
layout: post
---
#Shell脚本学习积累
* date命令
可以使用date -d解析时间字符串，如date -d ‘20180116’，在此基础上可以加上格式参数输入一定格式的时间，如date -d ‘20180116’ +%Y-%m-%d，这条语句将输出2018-01-16。也可以增加+%s，输出时间对应的UNIX时间戳。
* 调用函数
调用写好的Shell函数，如result=`test $1`。result后的等号两边不能有空格。
* 比较两个字符串的相等。需要使用x“$1” = x句式，等号两边的空格是不可缺少的
* 函数的返回
在使用`test $1`这种形式调用函数时，得到的结果是test函数中echo命令后边的内容

