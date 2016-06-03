---
layout: post
title: "Octopress Pluginで人気記事を表示する方法"
date: 2015-01-07
comments: true
categories: blog
tags: octopress
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">[popular_post.rb](https://github.com/satooshi/octopress-plugins/blob/master/plugins/popular_post.rb)というものがありました。<!--more--><br clear="all">

##はじめに

https://github.com/satooshi/octopress-plugins/blob/master/plugins/popular_post.rb

このプラグインは、 Google Analytics API を使って、記事のアクセス数を取得し、アクセス数が多い順に記事を表示することができるプラグインです。

以前書いた <a href="http://syui.github.io/blog/2014/12/28/google-analytics-2014/" target="_blank">Google Analytics API - MBA-HACK2</a> の記事を理解されている場合は、大体の仕組みが把握できるものと思われます。当該プラグインの導入に困った場合は、読んでみると良いかもしれません。

このプラグインの導入で嵌りそうな箇所は、2つあります。一つは、バージョンの問題。もう一つは、環境変数の問題です。


<a href="http://blog.satooshi.jp/blog/2013/04/05/octopress-popular-post-plugin-based-on-google-analytics-api/" target="_blank">Google Analytics APIを使ってOctopressで人気記事を表示するプラグインを書いた - satooshi@blog</a>

##Google Analytics API

[Google Console](https://code.google.com/apis/console/)を使って、APIを使えるようにしておき、JSONをダウンロードします。スクリプトディレクトリに`client_secrets.json`として保存します。

![](http://lh3.ggpht.com/-cS_i9Nfu5bs/VJ-vw6aQo-I/AAAAAAAAAM0/MrDsrCjqIiQ/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

![](http://lh3.ggpht.com/-txBeuq2Zmnw/VJ-vxVZePzI/AAAAAAAAAM4/BZK5yKKijZE/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

![](http://lh4.ggpht.com/-8zVc2PQtiLc/VJ-vwS4bXEI/AAAAAAAAAMs/FydjN9B655c/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)


###バージョンの問題

以下を追記して`bundle install`または、`bundler`します。

{% codeblock lang:bash octopress/Gemfile %}
gem "google-api-client", "0.6.4"
{% endcodeblock %}

`jwt`は、`0.1.5`で動きました。これは、`google-api`コマンドを実行するためのものです。

{% codeblock lang:bash octopress/Gemfile.lock %}
jwt (0.1.5)
{% endcodeblock %}

これで、以下のコマンドが実行できると思います。

{% codeblock lang:bash %}
# xxxxxx には client_secrets.json の情報を入れる
$ google-api oauth-2-login --client-id='xxxxxx' --client-secret='xxxxxx' --scope="https://www.googleapis.com/auth/analytics.readonly"

または、

# jq をインストールしている場合は、以下のコマンドにて自動で読み取れる。これは、 client_secrets.json がある場所で実行する
$ google-api oauth-2-login --client-id=`jq '.installed.client_id' ./client_secrets.json -r` --client-secret=`jq '.installed.client_secret' ./client_secrets.json -r` --scope="https://www.googleapis.com/auth/analytics.readonly"
{% endcodeblock %}

ブラウザが開きますので、承認すると、`~/.google-api.yaml`が保存されます。

###環境変数の問題

プラグインのコードを見てみると、環境変数は、`ENV`ということで、シェルから代入されるみたいです。なので、シェルの設定ファイルに以下を追加します。

{% codeblock lang:bash ~/.zshrc %}
# Analytics profile ID.
# https://www.google.com/analytics/web/home/a42353636w43552078pXXXXXXXX/
# URLのpのあと数字がProfile ID
export GOOGLE_ANALYTICS_PROFILE="ga:XXXXXXXX"
export GOOGLE_API_HOME="${HOME}/.google-api.yaml"
{% endcodeblock %}

###必要なファイルの保存

{% codeblock lang:bash %}
$ cd ~/blog/octopress/plugins/

$ curl -O https://raw.githubusercontent.com/satooshi/octopress-plugins/master/plugins/popular_post.rb

$ cd ~/blog/octopress/source/_includes/custom/asides/

$ curl -O https://gist.githubusercontent.com/satooshi/5318094/raw/analytics_popular_posts.html
{% endcodeblock %}

これで、`rake generate`が通るようになったかと思われますので、実行してみるのもよいでしょう。設定ファイルを書いてからでも構いませんが。

ちなみに、私の場合は、サイドバーを装飾しているので、以下のような感じで編集しています

{% codeblock lang:html octopres/source/_includes/custom/asides/analytics_popular_posts.html %}
{% raw %}
<section class="panel panel-default">
  <div class="panel-heading">
    <div class="panel-title">Popular Posts</div>
  </div>
  <div id="recent_posts" class="list-group">
    {% for post in site.popular_posts limit: 10 %}
    <a class="list-group-item {% if post.url == page.url %}active{% endif %}" href="{{ post.url }}">{% if site.titlecase %}{{ post.title | titlecase }}{% else %}{{ post.title }}{% endif %}</a>
    {% endfor %}
  </div>
</section>
{% endraw %}
{% endcodeblock %}

###プラグインの設定

{% codeblock lang:bash _config.yml %}
# サイドバーに表示する
default_asides: [ custom/asides/analytics_popular_posts.html ]

# 人気記事を表示する数の指定
popular_posts: 10
{% endcodeblock %}

