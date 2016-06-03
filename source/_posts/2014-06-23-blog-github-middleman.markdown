---
layout: post
title: "MiddlemanでGitHub Pagesを構築してみた"
date: 2014-06-23
comments: true
categories: [blog]
tags: [github, middleman, git]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Octopress よりも導入が簡単な Middleman を使ってみました。<!--more--><br clear="all">

##Middleman

<a href="http://middlemanapp.com/jp/" target="_blank">http://middlemanapp.com/jp/</a>

`Middleman`とは、簡単に言うとページの構築をコマンドラインから簡単に行うためのものです。

ドキュメントが日本語で丁寧に書かれているため、使い方が分からないということは少ないと思いますが、基本的な使い方は、以下の通りです。

{% codeblock lang:bash %}
# Web ページ作成の簡易化ツール Middleman のインストール
$ gem install middleman
$ gem install middleman-blog

# 指定のディレクトリにテンプレートを作成するコマンド
$ middleman init ~/hoge

# 現在のディレクトリにある source フォルダをプレビューを行うコマンド(http://localhost:4567/)
$ middleman server

# 現在ディレクトリの source フォルダ build フォルダ内に HTML 変換するコマンド
$ middleman build
{% endcodeblock %}

以下、自分がページを作った際の具体的な手順を紹介します。

###GitHub Pages の作成

まずは、 Middleman を使ってできるページのソース群をホスティングするための [GitHub Pages](https://pages.github.com/) を作りましょう。

ここでは、ユーザーページ(グループページも含む)、プロジェクトページがあるうちの、プロジェクトページを使用します。

それぞれのURLは、ユーザーページが`username.github.io`となっています。プロジェクトページが`username.github.io/reponame`となっています。

したがって、まずは、GitHub Pages(プロジェクトページ版) を作るために、新しいリポジトリを作成します。リポジトリ名はなんでもいいのですが、これが URL になります。ここでは、`middleman`としました。

次に、 `Settings > GitHub Pages > Automatic Page Generator`と進み、プロジェクトページを作成します。



プロジェクトページが作成されたら、`username.github.io/reponame`でアクセスできますので、アクセスしてみてください。

なお、私の場合は、以下のような URL になりました。

<a href="http://syui.github.io/middleman" target="_blank">http://syui.github.io/middleman</a>

###Middleman のインストールと使用

次に、 Middleman をインストールし、実際に使ってみます。

{% codeblock lang:bash %}
$ gem install middleman

$ gem install middleman-blog

$ middleman init ~/middleman

$ cd !$

$ middleman server

$ middleman build
{% endcodeblock %}

###Middleman を実行したフォルダに GitHub Pages をホスティングする

{% codeblock lang:bash %}
$ echo 'gem "middleman-deploy"' >> Gemfile

$ bundle

$ vim config.rb
{% endcodeblock %}

あとは、デプロイ自動化のための設定を書きます。以下を追記してください。

{% codeblock lang:ruby config.rb %}
configure :build do
  activate :asset_host, :host => "/reponame"
end

activate :deploy do |deploy|
  deploy.build_before = true
  deploy.method = :git
  deploy.branch = 'gh-pages'
end
{% endcodeblock %}

ここで、`/reponame`は、私の場合、`/middleman`になりますね。

内容を見てわかると思いますが、リポジトリに GitHub Pages(プロジェクトページ) を作った場合、以下のコマンドで作成したページを編集できます。

{% codeblock lang:bash %}
# リポジトリのクローン
git clone https://github.com/syui/middleman
cd !$:t

# ブランチの確認
$ git branch -r

# ブランチを GitHub Pages に変更
$ git checkout gh-pages
$ ls
{% endcodeblock %}

つまり、 `middleman deploy`コマンドを使わなくても、ブランチを変更し、更にはそこにあるファイルを全て削除した上で、`~/middleman/build`フォルダ内にあるファイルを持ってきて`git push`すれば、 Middleman で作成したページを公開できるということです。

しかしそれでは面倒くさいので、上の作業を自動化するスクリプトを使ったほうがいいのです。当該スクリプトを使うには、設定ファイルに自身の設定を書けば良いわけですね。

さて、上の設定を書けば、以下のコマンドで、`./build`が`gh-pages`ブランチにデプロイされます。

{% codeblock lang:bash %}
$ middleman deploy
{% endcodeblock %}

あとは、作成した GitHub Pages の URL にアクセスしてみればページが表示されているはずです。

`username.github.io/reponame`

###Middleman のテンプレート

Middleman もいくつかのテンプレートがあるみたいです。

<a href="http://directory.middlemanapp.com/#/templates/all" target="_blank">http://directory.middlemanapp.com/#/templates/all</a>

テンプレートを使いには、以下のコマンドのようにやります。

{% codeblock lang:bash %}
$ middleman init my_new_mobile_project --template=html5
{% endcodeblock %}

せめてデモページヘの URL は載せておいてほしい...。これは、プレビューするまでわからないという感じなのでしょうか。

参考:

<a href="http://www.adventar.org/calendars/251" target="_blank">Middleman Advent Calendar 2013 - Adventar</a>

<a href="http://d.hatena.ne.jp/osyo-manga/20140209/1391955805" target="_blank">middleman で構築したサイトを GitHub Pages で公開するまでの流れをまとめてみた - C++でゲームプログラミング</a>

<a href="http://nobuhito.github.io/env/2013/10/22/middleman/" target="_blank">GithubPagesとMiddlemanで技術系っぽいBLOGを始めて見る::Route4610</a>

###Middleman Blog

ブログも簡単に作成できます。具体的には、必要なモジュールをインストールした上で、`middleman init myproject --template=blog`コマンドとブログの設定を`config.rb`に書きます。

{% codeblock lang:ruby config.rb %}
Time.zone = "Tokyo"

activate :blog do |blog|
  # blog.prefix = "blog"
  # blog.permalink = ":year/:month/:day/:title.html"
  # blog.sources = ":year-:month-:day-:title.html"
  # blog.taglink = "tags/:tag.html"
  # blog.layout = "layout"
  # blog.summary_separator = /(READMORE)/
  # blog.summary_length = 250
  # blog.year_link = ":year.html"
  # blog.month_link = ":year/:month.html"
  # blog.day_link = ":year/:month/:day.html"
  # blog.default_extension = ".markdown"

  blog.tag_template = "tag.html"
  blog.calendar_template = "calendar.html"

  # blog.paginate = true
  # blog.per_page = 10
  # blog.page_link = "page/:num"
end
{% endcodeblock %}


参考:

<a href="http://rochas.cc/blog/2013/11/19/middleman-heroku.html" target="_blank">Middleman + Slim + Herokuでブログをつくりました - ROCHAS</a>
