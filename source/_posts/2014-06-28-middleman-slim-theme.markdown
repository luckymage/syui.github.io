---
layout: post
title: "Middlemanのテンプレートを使うときのarticle.url"
date: 2014-06-28
comments: true
categories: [blog]
tags: [middleman, github]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">めちゃくちゃハマりました。何故か、 article.url だけ先頭に / が来る仕様で、プロジェクトページを使った場合にパスの記述が上手くいかない問題について。<!--more--><br clear="all">

##一般的なpathの問題

> 問題 : 私は、ルートをOctopressで構築しているため、`/middleman`以下にページを作成することを考えました。しかし、デフォルトの設定では、なかなかパス設定が上手く行きませんでした。

上手く言った設定は以下の通り。`asset_hash`を設定してやると良いみたいです。

{% codeblock lang:ruby ./config.rb %}
set :site_url, 'http://syui.github.io/middleman'

activate :blog do |blog|
  blog.prefix = "blog"
  #blog.sources = "{year}-{month}-{day}-{title}.html"
  blog.tag_template = "tag.html"
  blog.calendar_template = "calendar.html"
end

configure :build do
  activate :asset_host, :host => "/middleman"
  activate :asset_hash
  set :relative_links, true
end
{% endcodeblock %}

更に、ところどころに`/`をそのまま記述しているところがあったので、`$ grep -R "'/'" .`など検索をして、その箇所を`#{site_url}`に変更しました。

ちなみに、 Middleman の記事は、`$ middleman article TITLE`で作成し、上記の設定だと`syui.github.io/middleman/blog`以下にポストされます。

この辺り、`blog.prefix`をプロジェクト名にするのだと勘違いしていました。

##article.urlの問題

> 問題 : プレビューでは上手くアクセスできているのに、実際に公開されると、「続きを読む」のリンクからはアクセス出来ない現象が起こりました。

そこで、`./build/index.html`をみてみると、`続きを読む`のところだけ、リンクの先頭に`/`が来ているようでした。

したがって、`./source/index.html.slim`を確認してみると、どうやら個別記事の URL が入っている`article.url`を使っているみたいでした。

つまり、通常の略式記述では、`{tag}/{title}.html`となるところが、`article.url`だと、`/tag/title.html`となってしまているのです。

時間がかかった理由としては、プレビューで確認できませんできないため、`push`しまくって地道に確認していくやりかたしか思いつきませんでした。

また、最初なので、[slim](https://github.com/yterajima/middleman-slim)の記述から何から何までよくわかりませんでした。

最終的には、`article.url`の辺りを以下のように変更しました。具体的には、`link_to article`を使います。

{% codeblock lang:html ./source/*.slim %}
  = article.summary
  = link_to 'Read more…', article
{% endcodeblock %}

とりあえず、応急処置としてはこんな感じで。疲れました...。

http://syui.github.io/middleman/

