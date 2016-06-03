---
layout: post
title: "gitbook-page"
date: 2015-03-10
comments: true
categories: blog
tags: github
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">GitBookを使ってみたので、メモ。<!--more--><br clear="all">

![](http://lh3.ggpht.com/-yj041MvVrNc/VP7xXNWI2uI/AAAAAAAAAiw/k-PPhl9yrR0/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588.png)

https://www.gitbook.com/

{% raw %}
    sudo npm update && sudo npm install gitbook -g && git clone https://github.com/onigra/gitbook-sample && cd gitbook-sample && sudo gitbook build && sudo gitbook serve
{% endraw %}

{% codeblock lang:bash %}
$ sudo npm update

$ sudo npm install gitbook -g

$ git clone https://github.com/onigra/gitbook-sample

$ cd gitbook-sample

$ sudo gitbook build

$ sudo gitbook serve
{% endcodeblock %}
