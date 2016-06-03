---
layout: post
title: "octopress-update"
date: 2015-04-19
comments: true
categories: blog
tags: octopress
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Octopressをアップデートすることで、無事、ビルドできました。<!--more--><br clear="all">

時間があったので、Octopressのアップデート及び、プラグインの修正などを行いました。

{% codeblock lang:bash %}
# octopress-update
$ git clone git://github.com/imathis/octopress.git octo-new

$ cd octo-new

$ rvm use 1.9.3

$ gem i bundler

$ bundle

$ rake install

$ rake preview
C-c

# octopress-origin-template
$ cd ..

$ git clone https://github.com/syui/syui.github.io

$ mv syui.github.io octo-old

$ cd octo-old

$ git checkout theme

$ rm -rf ../octo-new/{sass,source}

$ cp -rf {sass,source} ../octo-new

$ cat Gemfile >> ../octo-new/Gemfile

$ cd ../octo-new

$ vim Gemfile

$ bundle

$ rake generate

# エラーがでるので、必要なプラグインを置く
$ cp ../octo-old/plugins/{appbox.rb,tag_cloud.rb,tab_generator.rb,tocGenerator.rb} ./plugins/

# popular_posts.rbがエラーを出す
$ cp ../octo-new/plugins/popular_posts.rb ./plugins/
{% endcodeblock %}

今回遭遇したエラーは主に以下のような感じ。

{% codeblock lang:bash %}
1. ruby_executable_hooks:15: stack level too deep (SystemStackError)
        plugins/popular_posts.rb L157 alias_method comment-out.

2. Error: Pygments can't parse unknown language: </p>.
        plugins/pygments_code.rb L27  raise "Pygments can't parse unknown language: #{lang}#{code}."
{% endcodeblock %}

解決方法は2行目に載せてありますが、単純に、`1.`がコメントアウトと、`.analytics-cache`を持ってくることで解決。

`2.`は、コードを編集し、`rake gen`して結果を見ることで、問題の記事を探しだし、取り除くことで解決しています。

ちなみに、`popular_posts.rb`は、Shellの環境変数が必要だったり、Google APIのシークレットキーである`.google-api.yaml`が必要だったりと、いろいろと必要なものが多いプラグイン。

これは、主に、Google Analyticsからアクセス数の多い記事を取得し、サイドバーにするものです。

結構時間かかりましたが、OctopressのUpdateは終了です。デプロイしてみます。

