---
layout: post
keywords: Centos,Linux,diff
description: linux下比较文件diff的使用方法
title: "diff使用方法"
categories: [centos]
tags: [centos,linux,diff]
group: archive
icon: file-alt
---
{% include site/setup %}

###在linux下比较两个文件或者两个目录的不同，可以使用diff命令，下面记录一些例子：  

1、比较两个文件的差异  

    diff 1.txt 2.txt
    
>2c2  
>line 2 : differences  1.txt第二行的内容   
>line 2                2.txt第二行的内容  

2、比较两个文件的差异，只列出有无差异，并不显示详细信息  

`diff -q 1.txt 2.txt`  
Files 1.txt and 2.txt differ  
>只指出两个文件有所不同  

3、比较两个文件，将两个文件的全部内容分别显示在左右两侧  

`diff -y 1.txt 2.txt`  
line 1                 line1  
line 2:differences     |line 2  
1.txt的文件内容          2.txt的文件内容  

4、比较两个文件，仅在左侧显示相同内容，在两侧显示不同内容  

`diff -y --left-column 1.txt 2.txt`  
line 1  
line 2  
line 3 : differences        |line 3  

5、比较两个文件，只将不同的行显示在左右两侧  

`diff -y -suppress-common-line 1.txt 2.txt`  
line 2 : differences  | line 2  

6、显示两文件不同处，同时显示不同处前后的内容  

`diff -c 1.txt 2.txt`  

7、比较两个文件，显示不同处前后各两行的内容，并标出这两个文件不同处  

`diff -c -2 1.txt 2.txt`  

8、比较两个文件，显示不同处前后部分的内容，并将结果以合并的方式列出  

`diff -u 1.txt 2.txt`  

9、比较两个文件的不同，并显示不同处前后各行的内容，并将结果以合并的方式列出  

`diff -U 2 1.txt 2.txt`  

10、比较两个目录的不同  

`diff dir1 dir2`  

11、忽略内容中大小写的差异  

`diff -is dir1 dir2`  

12、比较两个目录中的文件时，若文件中包含question字符串，则忽略不比较此行  

`diff -l question -s dir1 dir2`  

13、比较两个目录中的文件，并以并列方式显示文件的不同之处  

`diff -y --suppress-common-lines dir1 dir2`  

14、比较两个目录下文件的不同，并比较子目录  

`diff -r dir1 dir2`  

15、比较两个目录下文件的不同，比较时忽略名称为file1的文件  

`diff -x file1 dir1 dir2`  

16、比较两个文件的不同，忽略空格数的不同  

`diff -b 1.txt 2.txt`  

17、比较两个文件的不同，忽略空行的不同  

`diff -B 1.txt 2.txt`  

18、比较二进制文件  

`diff -a 1.txt 2.txt`  

19、a.c和b.c是C语言的代码文件，比较两者不同，不一样的地方，列出不同的函数  

`diff -p a.c b.c`  

20、比较两个文件并忽略空白字符和空白行，且当文件相同时仅显示左侧文件内容  

`diff -bBy --left-column 1.txt 2.txt`  

其他，参考man手册。
