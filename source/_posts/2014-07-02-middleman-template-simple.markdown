---
layout: post
title: "middleman-simple-template"
date: 2014-07-02
comments: true
categories: [blog]
tags: [middleman, template, github]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Middlemanのテンプレートを作りました。まだ完成していませんが、公開作業をしたほうが、作業が進みやすいので。<!--more--><br clear="all">

##middleman-simple-template

{% githubrepo syui/middleman-simple-template %}

###インストール

{% codeblock lang:bash %}
$ git clone https://github.com/syui/middleman-simple-template

$ cd !$:t

$ bundle

$ middleman server
{% endcodeblock %}

Octopressが動作するものと同じバージョンを使いました。

``` bash "Ruby --version"
$ rvm install 1.9.3

$ rvm use 1.9.3
```

`Gemfile`が用意されているので、必要なツールをインストールします。

ここで、使っていないものも書き込んでいますが、後で整理する予定です。

``` bash "Ruby Bundler"
$ ls
> Gemfile

$ gem i bundler

$ bundle
```

###ScreenShot





###GitHub Pages

プロジェクトページで作成する場合は、新しいリポジトリを作成し、そこに GitHub Pages を作りましょう。リポジトリ名が URL になります。

具体的には、`http://USERNAME.github.io/REPOSITORY_NAME`のような感じです。



あとは、`./config.rb`の以下の項目の大文字の部分を変更すれば良いです。

{% codeblock lang:ruby config.rb %}
set :site_url, 'http://USERNAME.github.io/REPOSITORY_NAME'

# Build-specific configuration
configure :build do
  #activate :gzip
  activate :minify_css
  activate :minify_javascript
  activate :asset_host, :host => "/REPOSITORY_NAME"
  activate :asset_hash
  set :relative_links, true
end

activate :deploy do |deploy|
  deploy.build_before = true
  deploy.method = :git
  deploy.branch = 'gh-pages'
end
{% endcodeblock %}

