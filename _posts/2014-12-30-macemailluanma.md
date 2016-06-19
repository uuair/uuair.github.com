---
layout: post
keywords: Mac,Email
description: Mac Email乱码
title: "Mac Email.app程序乱码"
categories: [Mac]
tags: [mac,email]
group: archive
icon: file-alt
---
{% include site/setup %}

Mac自带的Email软件，在发送邮件的时候，尤其是发送给英文系统的中文邮件，经常会出现乱码的情况，本文就是解决这样的问题。(ps:我没测试过yosemite是否还有这个问题，虽然我一直在用，但我一直也使用了如下的方法保证email没有乱码)  

####第一种方法:  

    defaults write com.apple.mail NSPreferredMailCharset "GBK" 
    defaults write com.apple.mail NSPreferredMailCharset "UTF-8"
    defaults write com.apple.mail NSPreferredMailCharset "EUC"
    defaults write com.apple.mail NSPreferredMailCharset "GB18030" 
    //输入上面一行后，再开启 Mail 收发邮件就正常了。如果要还原设置，输入下面一行  
    defaults write com.apple.mail NSPreferredMailCharset "UTF-8"  
    
####第二种办法：  

一般自带的Email.app程序会出现乱码的情况，换第三方也许会好，但我还是爱用自带的，所以有了下面这个我一直用的办法:  

将下面的符号加到邮件的正文中:  
加入符号：⌘  

我一直都加在签名里:
例如：⌘Send from Uuair  

当然，还可以加入其他utf-8的符号，网上可以搜到很多，我列举几个：  
 ` Ⓐ Ⓑ Ⓒ Ⓓ Ⓔ Ⓕ Ⓖ Ⓗ Ⓘ Ⓙ Ⓚ Ⓛ Ⓜ Ⓝ Ⓞ Ⓟ Ⓠ Ⓡ Ⓢ Ⓣ Ⓤ Ⓥ Ⓦ Ⓧ Ⓨ Ⓩ ⓐ ⓑ ⓒ ⓓ ⓔ ⓕ ⓖ ⓗ ⓘ ⓙ ⓚ ⓛ ⓜ ⓝ ⓞ ⓟ ⓠ ⓡ ⓢ ⓣ ⓤ ⓥ ⓦ ⓧ ⓨ ⓩ ⓪ ⓫ ⓬ ⓭ ⓮ ⓯ ⓰ ⓱ ⓲ ⓳ ⓴ ⓵ ⓶ ⓷ ⓸ ⓹ ⓺ ⓻ ⓼ ⓽ ⓾ `

