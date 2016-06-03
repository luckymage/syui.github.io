---
layout: post
title: "Best Website Templates for 2015"
date: 2015-03-09
comments: true
categories: blog
tags: [hugo,middleman,jekyll]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">おすすめのテンプレートを紹介します。<!--more--><br clear="all">

##hugo-incorporated

[hugo](https://github.com/spf13/hugo)を使います。

https://github.com/nilproductions/hugo-incorporated

![](http://lh5.ggpht.com/-Jd1zx4Gfy1I/VP1mCDPn2qI/AAAAAAAAAhk/o3_XnvanCgc/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

###ワンライナー

{% raw %}
    git clone https://github.com/nilproductions/hugo-incorporated && cd hugo-incorporated &&  mkdir -p themes/hugo-incorporated/static && hugo server -w
{% endraw %}

{% codeblock lang:bash 解説 %}
# hugo のインストール
$ export GOPATH=$HOME/go
$ go get -v github.com/spf13/hugo

$ git clone https://github.com/nilproductions/hugo-incorporated

$ cd hugo-incorporated

$ mkdir -p themes/hugo-incorporated/static

$ hugo server -w
{% endcodeblock %}

##lanyon-hugo


こちらも、[hugo](https://github.com/spf13/hugo)を使います。

http://tummychow.github.io/lanyon-hugo/

![](http://lh5.ggpht.com/-YDreUnZcCxU/VP1mBSNOm2I/AAAAAAAAAhg/hgAWGj5ZsLk/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

###ワンライナー

{% raw %}
    git clone https://github.com/tummychow/lanyon-hugo && cd lanyon-hugo && sed -i "" 's#"baseurl": "http://tummychow.github.io/lanyon-hugo/"#"baseurl": "http://tummychow.github.io"#g' config.json && hugo server
{% endraw %}

###解説

{% codeblock lang:bash %}
{% raw %}
$ git clone https://github.com/tummychow/lanyon-hugo

$ cd lanyon-hugo

$ sed -i "" 's#"baseurl": "http://tummychow.github.io/lanyon-hugo/"#"baseurl": "http://tummychow.github.io"#g' config.json

$ hugo server
{% endraw %}
{% endcodeblock %}

##davidl

こちらは、[Middleman](https://middlemanapp.com/)を使います。

https://github.com/flexbox/davidl

![](http://lh3.ggpht.com/-kag6ZxI-7xE/VP1oGwP-OPI/AAAAAAAAAhw/_L72re3rUA0/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588.png)


###ワンライナー

{% raw %}
    git clone https://github.com/flexbox/davidl && cd davidl && bundle install && bower install && middleman server 
{% endraw %}

###解説

{% codeblock lang:bash %}
$ ruby --version
ruby 2.1.5p273

#rvm install 2.1.5
#rvm use 2.1.5

$ gem install middleman

$ bundle install

$ bower install

$ middleman server 
{% endcodeblock %}


##landing-page-theme

こちらは、[jekyll](http://jekyllrb.com/)です。

https://github.com/swcool/landing-page-theme

![](http://lh6.ggpht.com/-l2duHbXqf7M/VP1o84_Z_MI/AAAAAAAAAh4/B7z6Pq8Ei_0/s0/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588.png)

###ワンライナー

{% raw %}
    git clone https://github.com/swcool/landing-page-theme && cd landing-page-theme && gem install jekyll && jekyll server
{% endraw %}

###解説

{% codeblock lang:bash %}
$ ruby --version
ruby 2.0.0p598

#rvm install 2.0.0
#rvm use 2.0.0

$ git clone https://github.com/swcool/landing-page-theme

$ cd landing-page-theme

$ gem install jekyll

$ jekyll server
{% endcodeblock %}

