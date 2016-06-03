---
layout: post
title: "Octopressで見出しタグを目次にしてみる"
date: 2014-07-06
comments: true
categories: [blog]
tags: [github, octopress, jekyll]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100"> jekyll-toc-generator を使います。<!--more--><br clear="all">

##jekyll-toc-generator



###Download

{% githubrepo dafi/jekyll-toc-generator %}

{% codeblock lang:bash %}
$ cd ~/octopress/plugins

$ curl -O https://raw.githubusercontent.com/dafi/jekyll-toc-generator/master/_plugins/tocGenerator.rb

# 目次を作る見出しタグの種類を変更する(Default:h1, h2)
$ sed -i "" -e 's/h2/h3/g' -e 's/h1/h2/g' !$:t

$ cd ~/octopress/source/javascripts

$ curl -O https://raw.githubusercontent.com/dafi/jekyll-toc-generator/master/js/jquery.tocLight.js
{% endcodeblock %}

###HTML

`Articles`などの独立ページでも使用したければ、`page.html`にも記述します。

`content`の部分を変更します。`body`内に記述されています。

{% codeblock lang:html octopress/source/_layouts/default.html,page.html %}
{% raw %}
<div id="content">
  {{ content | expand_urls: root_url | toc_generate }}
</div>
{% endraw %}
{% endcodeblock %}

###CSS

CSSもデフォルトで用意されていますので、適応したい方は、適応しましょう。

{% codeblock lang:bash %}
{% raw %}
$ curl -o ~/octopress/sass/partials/toc.css https://raw.githubusercontent.com/dafi/jekyll-toc-generator/master/css/toc.css

$ echo '@import "partials/toc";' >> ~/octopress/sass/_partials.scss
{% endraw %}
{% endcodeblock %}

###Setting

表示したくない時は、個別記事に`noToc: true`のオプションを付けます。

{% codeblock lang:bash %}
layout: post
title: "Octopressで見出しタグを目次にしてみる"
date: 2014-07-06
comments: true
categories: [blog]
tags: [github, octopress, jekyll]
noToc: true
{% endcodeblock %}


参考:

<a href="http://blog.chopschips.net/blog/2014/06/16/octopress-toc/" target="_blank">Octopressで見出しの目次を作る方法 - 割り箸ポテチ</a>

