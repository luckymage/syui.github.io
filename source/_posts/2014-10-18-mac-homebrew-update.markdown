---
layout: post
title: "Yosemite前にHomebrewをアップデートした"
date: 2014-10-18
comments: true
categories: os
tags: [package, mac]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">色々アップデートされました。<!--more--><br clear="all">

{% codeblock lang:bash %}
$ brew update && brew upgrade

# opensslもアップデートされ、rvmで使ってるのでrvmのアップデートも行います
$ rvm reinstall 1.9.3
{% endcodeblock %}

[Symbol not found: _SSLv2_client_method (LoadError)](http://stackoverflow.com/questions/25492787/ruby-bundle-symbol-not-found-sslv2-client-method-loaderror)

