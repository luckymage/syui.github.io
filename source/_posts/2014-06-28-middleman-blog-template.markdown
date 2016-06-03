---
layout: post
title: "Middlemanのブログテンプレートを使ってみた"
date: 2014-06-28
comments: true
categories: [blog]
tags: [middleman, bower, github, ruby]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Middlemanでブログを構築するのは思った以上に簡単でした。<!--more--><br clear="all">

##Middlemanについて

[Middleman](http://directory.middlemanapp.com/) とは、 [Octopress](http://octopress.org/) 同様、コマンドラインから静的ページを簡単に構築するためのツールです。

[Template](http://directory.middlemanapp.com/#/templates/all) も豊富で、 Octopress よりも手順が簡略化され、かつ各モジュールのバージョンも最新に近い状態なので、人気があります。

###middleman-blog-bootstrap-template

####テンプレートのインストール

今回は、[middleman-blog-bootstrap-template](https://github.com/biblichor/middleman-blog-bootstrap-template) というテーマを使ってみます。

Ruby のバージョンは、`2.1.2`を使うことにします。このテンプレートでは、[bower](https://github.com/bower/bower)も使っているようですね。

テンプレートを使うための手順は、まず、`~/.middleman`以下のディレクトリにテンプレートを置きます。そして、そのディレクトリ名で`middleman init プロジェクト名 --template=テンプレートのディレクトリ名`というコマンドを実行します。

すると、プロジェクト名のディレクトリが現在ディレクトリに作成されますので、その中から`middleman`の各種コマンドを実行します。

{% codeblock lang:bash %}
$ rvm install 2.1.2

$ rvm use 2.1.2

$ gem install middleman

$ git clone https://github.com/biblichor/middleman-blog-bootstrap-template.git ~/.middleman/blog-bootstrap

$ middleman init my_new_project --template=blog-bootstrap

$ cd my_new_project

$ bundle

$ npm install -g bower

$ bower install
{% endcodeblock %}

####Gemfile

必要なモジュールは、`Gemfile`に書き、`bundle install`で導入します。

現時点では以下の様な感じです。`Markdonw`や`Syntax-Highlighting`などを使いたい場合は、各自導入する必要があります。たぶん。

{% codeblock lang:ruby ./Gemfile %}
# If you have OpenSSL installed, we recommend updating
# the following line to use "https"
source 'http://rubygems.org'

gem "middleman", "~> 3.2.2"
gem "middleman-blog", "~> 3.5.1"
gem "middleman-target", "~> 0.0.6"
gem "middleman-deploy", "~> 0.1.4"

# Live-reloading plugin
gem "middleman-livereload", "~> 3.1.0"

# For Slim
gem "slim", "~> 2.0.2"

# For Markdown
gem "redcarpet", "~> 3.1.1"

# For blog summary
gem "nokogiri", "~> 1.6.1"

# For feed.xml.builder/sitemap.xml.builder
gem "builder", "~> 3.0"
{% endcodeblock %}

####config.rb

設定は、`config.rb`に書きます。とりあえずは、デプロイ簡易化の設定を書いておきます。

なお、デプロイ簡易化の設定は、`gem "middleman-deploy"`モジュールが必要になります。

{% codeblock lang:ruby ./config.rb %}
configure :build do
  # For example, change the Compass output style for deployment
  activate :asset_host, :host => "/middleman"
  activate :minify_css

  # Minify Javascript on build
  activate :minify_javascript

  # Enable cache buster
  # activate :asset_hash

  # Use relative URLs
  activate :relative_assets
  set :relative_links, true
end

  # Or use a different image path
  # set :http_prefix, "/Content/images/"
  activate :deploy do |deploy|
  deploy.build_before = true
  deploy.method = :git
  deploy.branch = 'gh-pages'
end
{% endcodeblock %}

ちなみに、デフォルトでは`#root`が`source/foo/index.html.erb`の中から相対パスなので、`link_to`で作られるあらゆる URL を相対パスにしたい場合の設定は以下の通りです。

{% codeblock lang:bash ./config.rb https://github.com/neo/middleman-gh-pages LINK %}
activate :relative_assets
set :relative_links, true
{% endcodeblock %}

私の場合は、`root`では、 Octopress を展開させていますので、以下のように書きます。ただし、これは、 GitHub Pages で構築するページの通常の設定ではありません。

{% codeblock lang:bash ./config.rb http://middlemanapp.com/jp/basics/helpers/ LINK %}
# Use relative URLs
# activate :directory_indexes
# activate :relative_assets
# set :relative_links, true
{% endcodeblock %}


参考:

http://middlemanapp.com/jp/basics/blogging/


####テンプレートのプレビューやビルド

{% codeblock lang:bash %}
# 現在のディレクトリにある source フォルダをプレビューを行うコマンド(http://localhost:4567/)
$ middleman server

# 現在ディレクトリの source フォルダ build フォルダ内に HTML 変換するコマンド
$ middleman build

# 指定されたホストにデプロイするコマンド
$ middleman deploy
{% endcodeblock %}


現時点では、一応こんな感じのテンプレートみたいです。



デプロイが上手くいかない場合は、[こちら](http://syui.org/blog/2014/06/23/blog-github-middleman/)の記事を参考にしてください。

####Middlemanのzsh completions

`zsh`の補完が効かなかったので、探してみました。こういうのは大体公式リポジトリに置いてあるので、インストールフォルダ探せば見つかるような気もしますが。

{% codeblock lang:bash %}
$ cd ~/.zsh/functions/

$ curl -O https://raw.githubusercontent.com/sshankar/dotx/master/.zsh/completions/_middleman

$ source ~/.zshrc
{% endcodeblock %}





