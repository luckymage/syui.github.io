---
layout: post
title: "Octopress"
date: 2014-03-26
comments: true
categories: [blog]
tags: [github, octopress, jekyll, markdown, html, css]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Octopressのカスタマイズ履歴です。このブログでは、テーマを一つに設定して、それを元にカスタマイズしていくというスタイルを採用します。<!--more--><br clear="all">

##目次

|番号|タイトル|タグ|
|--|--|--|
|00|[Octopressのインストール](#page00)|install, octopress, github
|01|[OctopressでのCode Block](#page01)|html, markdown, octopress
|02|[OctopressのMarkdownパーサー](#page02)|markdown, ruby
|03|[Markdown特殊記法](#page03)|markdown
|04|[Previewを高速化する](#page04)|ruby, preview
|05|[日付の形式を変更する](#page05)|data, html
|06|[Mobileの表示に対応する](#page06)|mobile, ios, android, browser
|07|[様々な記号を使う](#page07)|html
|08|[Top Pageに移動するアイコンを作った](#page08)|html, top, icon
|09|[Menubarの試行錯誤](#page09)|menu, html, css
|10|[スライド式のmore](#page10)|html, css
|11|[Comment Form Disqus](#page11)|disqus, comment
|12|[文章幅の調整](#page12)|font, css
|13|[Octostrap3のPager](#page13)|octopress, theme
|14|[Code Blockの行番号と背景色](#page14)|markdown, octopress
|15|[フォントの大きさ](#page15)|font, css
|16|[Archives](#page16)|octopress
|17|[AppStoreのアプリを紹介する](#page23)|app, store
|18|[スラッシュのような線](#page18)|border, css
|19|[codeのカスタマイズ](#page19)|css, code
|20|[Sidebarにいろいろ設置する](#page20)|sidebar, hatena, qiita, github
|21|[Div要素全体にリンクを貼る](#page21)|div, html
|22|[画像枠を変更する](#page22)|img, html
|23|[Amazonの紹介を簡単にする](#page24)|amazon
|24|[参考になるブログ](#page17)|blog, octopress
|25|<a href="http://syui.co/blog/2014/06/03/googleplus/" target="_blank">Google+との連携を考える</a>|別ページ
|26|<a href="http://syui.co/blog/2014/06/04/dns/" target="_blank">Octopressに独自ドメインを設定する方法</a>|別ページ


##<a name="page00">Octopressのインストール</a>

###はじめに

最近､[Octopress](http://octopress.org/)でブログをはじめました｡


`Octopress`は、[テーマ](http://opthemes.com/)も豊富で､[Middleman](http://middlemanapp.com/)よりも簡単な感じです｡

Octopressでのブログの初め方は､以下のページに書きました｡

[Github Pages + Octopress](http://mba-hack.blogspot.jp/2014/02/github-pages-octopress.html)

しかし、バージョンが更新されていないみたいで、[アップデート](http://blog.glidenote.com/blog/2014/02/14/octopress-update/)も面倒な感じがします｡

どちらを使うかは､好みの問題ですが､カスタマイズを楽にしたいのなら､`Octopress`がオススメです｡

テーマは､[octostrap3](https://github.com/kAworu/octostrap3)というものを使用することにします。

よって、この記事で紹介するカスタマイズは､すべて`octostrap3`というテーマを使ってのカスタマイズになります。

一方､最新のトレンドに追従したいのなら、`Middleman`がオススメです｡


なお、ここでは、主に、HTMLとCSSについてのコードを書いていきます。

一番参考になるページは、以下のページです。

<a href="https://developer.mozilla.org/ja/docs/Web" target="_blank">Web technology for developers | MDN</a>


####注意点

> メールアドレスの認証（verify）を事前に済ませておく必要がある。

> ページの構築に､10分ほど時間がかかる可能性がある｡

####リポジトリの作成


GitHubリポジトリを作成します。 リポジトリ名は「username.github.io」とします。

###Octopress Setup

{% codeblock lang:bash %}
$ git clone https://github.com/imathis/octopress

$ cd $!:t

$ gem install bundler

$ bundle install

$ rake setup_github_pages
{% endcodeblock %}


出来ない場合は､`rvm`などでRubyを1.9.3に変更してみます。

http://octopress.org/docs/setup/

###Octopress 初期設定

####基本設定

以下のファイルで基本設定が出来ます｡サイドバーなどもここで設定します｡

``` css _config.yml
url:                # For rewriting urls for RSS, etc
title:              # Used in the header and title tags
subtitle:           # A description used in the header
author:             # Your name, for RSS, Copyright, Metadata
simple_search:      # Search engine for simple site search
description:        # A default meta description for your site
date_format:        # Format dates using Ruby's date strftime syntax
subscribe_rss:      # Url for your blog's feed, defauts to /atom.xml
subscribe_email:    # Url to subscribe by email (service required)
category_feeds:     # Enable per category RSS feeds (defaults to false in 2.1)
email:              # Email address for the RSS feed if you want it.
```

http://octopress.org/docs/configuring/

####Jekyll & Plugins

{% codeblock lang:css %}
root:               # Mapping for relative urls (default: /)
permalink:          # Permalink structure for blog posts
source:             # Directory for site source files
destination:        # Directory for generated site files
plugins:            # Directory for Jekyll plugins
code_dir:           # Directory for code snippets (for include_code plugin)
category_dir:       # Directory for generated blog category pages

pygments:           # Toggle python pygments syntax highlighting
paginate:           # Posts per page on the blog index
pagination_dir:     # Directory base for pagination URLs eg. /blog/page/2/
recent_posts:       # Number of recent posts to appear in the sidebar

default_asides:     # Configure what shows up in the sidebar and in what order
blog_index_asides:  # Optional sidebar config for blog index page
post_asides:        # Optional sidebar config for post layout
page_asides:        # Optional sidebar config for page layout
{% endcodeblock %}


###Octopress 記事作成とプレビュー

{% codeblock lang:bash %}
{% raw %}
$ rake new_post\[title\]

$ vim source/_post/*.markdown

$ rake preview

$ open -a Safari http://localhost:4000/
{% endraw %}
{% endcodeblock %}



http://octopress.org/docs/blogging/


```
rake generate   # Generates posts and pages into the public directory
rake watch      # Watches source/ and sass/ for changes and regenerates
rake preview    # Watches, and mounts a webserver at http://localhost:4000
```


####Octopress 記事投稿

記事を公開し､GitHubにpushしておきます｡

{% codeblock lang:bash %}
$ cd octopress/source

$ rake gen_deploy

$ git add .

$ git commit -m 'your message'

$ git push origin source
{% endcodeblock %}

http://octopress.org/docs/deploying/github/

####Octopress Themeの変更


{% codeblock lang:bash %}
$ cd octopress

$ git clone https://github.com/kAworu/octostrap3 .themes/octostrap3

$ rake 'install[octostrap3]'

$ rake generate
{% endcodeblock %}

###Octopressの基本的なカスタマイズ

ここでは、基本的なカスタマイズを紹介します。

####Preview thin

プレビューを変更してみます｡`group :development do`の後に､`gem 'thin'`を追記します｡


{% codeblock lang:bash %}
$ vim octopress/Gemfile

###########################
group :development do
gem 'thin'
###########################

$ bundle install

$ thin start
{% endcodeblock %}

あとは、ブラウザで`http://localhost:3000`にアクセスします。


####More

「続きを読む」には、`more`タグを使います。

{% codeblock lang:html %}
{% raw %}
<!-- more -->
{% endraw %}
{% endcodeblock %}

####About

新しいページを作成し､ナビバーに表示させます｡

{% codeblock lang:bash %}
$ rake 'new_page["about"]'
{% endcodeblock %}

{% codeblock lang:html source/_includes/custom/navigation.html %}
{% raw %}
<li><a href="/about">About</a></li>
{% endraw %}
{% endcodeblock %}


####Icon

ナビバーにアイコンを表示してみます｡

{% codeblock lang:html source/_includes/custom/navigation.html %}
{% raw %}
<img src="URL" alt="site.logo"><a class="navbar-brand" href="/">MBA-HACK</a>
{% endraw %}
{% endcodeblock %}

####Favicon

ファビコンというのは、タブのところに表示されているアイコンのことです。`.png`でもOKです。

{% codeblock lang:html source/_includes/custom/head.html %}
{% raw %}
<link href="URL" rel="icon">
{% endraw %}
{% endcodeblock %}

他にも､ルート`/`に`favicon.ico`を置くと、表示されるとかいう情報もあります｡

{% codeblock lang:bash %}
{% raw %}
$ convert favicon.png favicon.ico
{% endraw %}
{% endcodeblock %}

なお、モバイルのブックマークアイコンを設定するには､以下のようにします｡

{% codeblock lang:html source/_includes/custom/head.html %}
{% raw %}
<link href="URL" rel="apple-touch-icon" />
{% endraw %}
{% endcodeblock %}

####Delete

不要なアイコンを削除してみます｡`span`と`class`のiconがキーワードです｡

{% codeblock lang:html source/_includes/post/{date,sharing}.html %}
{% raw %}
<span class="glyphicon glyphicon-calendar"></span>
{% endraw %}
{% endcodeblock %}

####Pager

ページャーの角丸設定を削除します。


以下のファイルを見てみます。

{% codeblock lang:bash %}
$ cat source/index.html && cat source/assets/bootstrap/dist/css/bootstrap.css
{% endcodeblock %}

設定ファイルにソースを追記します｡


{% codeblock lang:bash %}
$ echo '@import "custom/_styles.scss";' >> sass/_base.scss
{% endcodeblock %}

以下のファイルに追記します｡

``` css sass/custom/_styles.scss
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 10px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
}
```


##<a name="page01">OctopressでのCode Block</a>

Octopressでの[Code Block](http://octopress.org/docs/plugins/backtick-codeblock/)は、現在､`linenos`には対応していません。


ちなみに、`linenos`というのは､行に関する設定のことです｡現在は､[startinline](https://github.com/imathis/octopress/blob/master/plugins/pygments_code.rb)という呼び方の方が正しいのかもしれません。


[公式ドキュメント](http://octopress.org/docs/blogging/code/)には､以下の様なCode Blockが使えるとされています｡

{% raw %}
    ``` coffeescript Coffeescript Tricks start:51 mark:52,54-55
    # Given an alphabet:
    alphabet = 'abcdefghijklmnopqrstuvwxyz'

    # Iterate over part of the alphabet:
    console.log letter for letter in alphabet[4..8]
    ```
{% endraw %}





しかし、行番号、マークなどのオプションは実際には使えません。


対応しているのは、[site-2.1](https://github.com/imathis/octopress/tree/site-2.1)ブランチのみです。


<a href="https://github.com/imathis/octopress/issues/1472" target="_blank">BUG: start, mark, and linenos don't work in code blocks · Issue #1472 · imathis/octopress · GitHub</a>

<a href="http://nhiroki.jp/blog/2013/11/11/octpress-codeblock" target="_blank">Octpress の codeblock でオプションが効かない - nhiroki's weblog</a>


##<a name="page02">OctopressのMarkdownパーサー</a>

Octopressでは、特定のフォルダ内にあるMarkdownの拡張子で書いたファイルは、自動で変換されます。この処理を行うツールをMarkdownパーサーといいます。

Markdownパーサーとして有名なのは､[Pacdoc](http://sky-y.github.io/site-pandoc-jp/users-guide/)です。私も変換の際は基本このツールを使っているのですが､Octopressのデフォルトでは､[RDiscount ](https://github.com/davidfstr/rdiscount)が採用されています｡


[http://rdoc.info/github/davidfstr/rdiscount/RDiscount](http://rdoc.info/github/davidfstr/rdiscount/RDiscount)


変更するには､jekyllの設定ファイルに書きます｡

``` ruby _config.yml
markdown: rdiscount
rdiscount:
  extensions:
    - autolink
    - footnotes
    - smart
```


###jekyllでのMarkdown設定

ここでは、[Redcarpet](https://github.com/vmg/redcarpet)を使ってみます｡


``` ruby _config.yml
markdown: redcarpet2
redcarpet:
  extensions: ["no_intra_emphasis", "fenced_code_blocks", "autolink", "strikethrough", "superscript", "with_toc_data"]
```

####bundle install

まず、`bundle install`を実行するために、`Gemfile`を編集します｡


###Markdownパーサーの機能

Markdownパーサーの機能はツールごとにそれぞれです｡


例えば､`autolink`の機能は、リンクがあれば自動でタグ付けしてくれます。


<a href="http://higelog.brassworks.jp/?p=1704" target="_blank">Rubyで使えるMarkdownパーサー | ひげろぐ</a>

<a href="http://blog.tdksk.com/2013/05/06/use-gfm-in-octopress.html" target="_blank">Octopress で GitHub Flavored Markdown (GFM) を使う - blog.tdksk.com</a>


##<a name="page03">Markdown特殊記法</a>

###codeblock

`codeblock`を使うことで､コードを綺麗に表示できます｡


####実行前

{% raw %}
    {% codeblock lang:ruby hello.rb %}
    puts "hello"
    {% endcodeblock %}
{% endraw %}

####実行後

{% codeblock lang:ruby hello.rb %}
puts "hello"
{% endcodeblock %}

###backtick

<code>`</code>を使うことで、コードをそのまま表示できます｡

####実行前

{% raw %}
    ``` ruby hello.rb http://syui.github.io/ LINK
    puts "hello"
    ```
{% endraw %}

####実行後

``` ruby hello.rb http://syui.github.io/ LINK
puts "hello"
```

backtickを単体で表示したい場合は､直接`<code>`などを使うと良いです｡


###raw

`raw`コードで囲むことで、特殊記法である`backtick`などを表示できます｡ただし、行頭に`Tab`または`Space`を二つ入れましょう。

####実行前

{% codeblock %}
{{"{"}}% raw %}
    ``` ruby hello.rb
    puts "hello"
    ```
{{"{"}}% endraw %}
{% endcodeblock %}

####実行後

{% raw %}
    ``` ruby hello.rb
    puts "hello"
    ```
{% endraw %}


HTMLを表示したい場合は、`codeblock`と`raw`を組み合わせるとうまくいきます。


ちなみに、`raw`は以下のコードを使うことで､`code`をエスケープできます。

{% raw %}
    {{"code"}}
{% endraw %}


<a href="http://rcmdnk.github.io/blog/2013/05/05/blog-octopress/" target="_blank">Octopressでのコードの表示やコメントのあれこれ - rcmdnk's blog</a>

###markdown

Markdownパーサーを指定できます｡



##<a name="page04">Previewを高速化する</a>

記事を読み込まれない場所に移動させることで､プレビューを高速化出来ます｡

{% codeblock lang:bash %}
$ rake isolate\[filename\]

$ rake integrate
{% endcodeblock %}


`isolate`は、指定したファイル以外を`source/_stash`に移動させるコマンドです｡


`integrate`は、移動させたファイルを元の場所に戻すコマンドです｡


[Octopressのpreviewを高速化する - gam0022.net](http://gam0022.net/blog/2013/09/28/speed-up-octopress-site-generation/)


###Previewと同時に､Browserを開く


``` ruby Rakefile
    require 'bundler/setup'
    require 'thread'
    require 'launchy'

    desc 'preview'
    task :preview do
      Thread.new do
        sleep 1
        Launchy.open 'http://localhost:4000/'
      end

      sh 'bundle exec jekyll serve --watch'
    end
```

``` ruby Gemfile
gem 'github-pages'
gem 'launchy'
```


<a href="http://blog.eiel.info/blog/2013/08/28/browse-open-when-rake-preview/" target="_blank">ローカルサーバ起動と同時にブラウザで開く。 - Jekyll とかで。 - そんなこと覚えてない</a>


##<a name="page05">日付の形式を変更する</a>

`_config.yml`の`date_format:`を編集します｡

``` ruby _config.yml
# 2014/01/01
date_format: "%Y/%m/%d"

# 2014年1月1日
date_format: "%Y年%m月%d日"
```

##<a name="page06">Mobileの表示に対応する</a>

ダウンロードしたテーマでは、モバイルサイトでバウンドしてしまうようです。したがって、出来る限りバウンドしないように設定します｡




ちなみに、モバイル設定は別にしてまとめておいたほうが良さそうです｡


``` css sass/custom/_mobile.scss
img {
word-break: break-all;
white-space: inherit;
}

figure {
word-break: break-all;
}

code {
word-wrap: break-word;
//word-break: break-all;
white-space: inherit;
}

a {
word-break: break-all;
}
```

原則として、`word-wrap: break-word`を使ったほうが良さそうです。Firefoxでは、一部、`word-wrap: break-word`でないと効果が無いケースを確認しました。



参考:

<a href="http://nanto.asablo.jp/blog/2013/06/18/6869571" target="_blank">長い英単語を途中で折り返したいときの CSS の指定方法: Days on the Moon</a>


``` css sass/_base.scss
@import "custom/_mobile";
```

##<a name="page07">様々な記号を使う</a>

以下のページがとても参考になりました｡

http://www.benricho.org/symbol/tokusyu_01_usefull.html

具体的には､`more`や`pager`に使用しました。

`more`は、`_config.yml`にて設定します。

`pager`は、`source/index.html`及び､`source/_layouts/post.html`にて設定します｡


##<a name="page08">Top Pageに移動するアイコンを作った</a>

たまに自分で閲覧していて、不便な時があるので設置することにしました。ヘッダー固定用。



{% codeblock lang:css %}
.mobile-footer-up {
z-index: 99999;
position: fixed;
bottom: 0px;
left: 0%;
width: 100%;
hight: 30px;
text-align: center;
font-size: 15px;
font-weight: 500;
background-color: #000;
color: #0066FF;
}

.mobile-footer-up a {
display: block;
}

.mobile-footer-up a:hover {
color: #66CCFF;
background-color: #303030;
}
{% endcodeblock %}


`index.html`の末尾に以下のコードを追加します｡

``` html source/index.html http://mba-hack.blogspot.jp/2013/11/blogger_27.html LINK
<div class='mobile-footer-up'><a href='#top'>&and;</a></div>
```

ちなみに、目次がある場合には、目次に飛ぶこともできます。

``` html source/_posts/test.markdown
<a name="top">目次</a>
```

## <a name="page09">Menubarの試行錯誤</a>

###Menubar Ver.1

結構、苦戦しました｡このテーマのメニューバーは､CSS要素で現在選択しているメニューを示します｡


HTMLは、デモサイトのソースを読みました｡


{% codeblock lang:html source/_includes/custom/navigation.html %}
{% raw %}
<ul class="nav navbar-nav">
    <li {% if page.navbar == 'Blog' %}class="active"{% endif %}>
        <a href="{{ root_url }}/"><img class="hidden-xs" src="{{ root_url }}/images/home.png" alt="home"></a>

    </li>
    <li {% if page.navbar == 'Archives' %}class="active"{% endif %}>
        <a href="{{ root_url }}/blog/archives">Archives</a>
    </li>
    <li {% if page.navbar == 'Twitter' %}class="active"{% endif %}><a href="https://twitter.com/PSP_T" target="_blank">Twitter</a></li>
    <li {% if page.navbar == 'About' %}class="active"{% endif %}><a href="{{ root_url }}/about">About</a></li>
</ul>
{% endraw %}
{% endcodeblock %}

CSSで新しく追加する要素は､`li:hover`と`.active:hover`です。

``` css sass/partials/_header.scss
.navbar {
margin-bottom: 40px;
border: 0;
}

.navbar-default .navbar-nav>.active>a {
color: #000;
background-image: -webkit-linear-gradient(top,#428bca 0,#428bca 100%);
background-image: linear-gradient(to bottom,#428bca 0,#428bca 100%);
  -webkit-box-shadow: none;
  box-shadow: none;
}

.navbar-nav > li:hover {
background-image: -webkit-linear-gradient(top,#428bca 0,#428bca 100%);
background-image: linear-gradient(to bottom,#428bca 0,#428bca 100%);
}

.navbar-nav > .active:hover {
opacity: 0.5;
transition: 0.7s;
background-image: -webkit-linear-gradient(top,#428bca 0,#428bca 100%);
background-image: linear-gradient(to bottom,#428bca 0,#428bca 100%);
}
```


###Menubar Ver.2

選択されたメニューに`1px`の齟齬があったり、`hover`の設定が難しかったりです｡

今のところ､以下の様な感じになっています。



{% codeblock lang:html source/_includes/custom/navigation.html %}
{% raw %}
<nav class="navbar navbar-default" role="navigation">
<div class="container2">
  <a href="/"><img src="{{ root_url }}/images/phoenix_fire.png" width="150" height="150" alt="phoenix_fire"></a>
</div>
    <div class="container">

        <div class="navbar-header">
            <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
           <a class="navbar-brand" href="{{ root_url }}/">{{ site.title }}</a>
        </div>

        <div class="navbar-collapse collapse">
            <ul class="nav navbar-nav">
                <li {% if page.navbar == 'Blog' %}class="active"{% endif %}>
                    <a href="{{ root_url }}/"><img src="{{ root_url }}/images/home.png" alt="home"></a>


                </li>
                <li {% if page.navbar == 'Archives' %}class="active"{% endif %}>
                    <a href="{{ root_url }}/blog/archives">Archives</a>
                </li>
                <li {% if page.navbar == 'Twitter' %}class="active"{% endif %}><a href="https://twitter.com/PSP_T" target="_blank">Twitter</a></li>
                <li {% if page.navbar == 'About' %}class="active"{% endif %}><a href="{{ root_url }}/about">About</a></li>
            </ul>
            <ul class="nav navbar-nav navbar-right">
                <li>
                    <a class="subscribe-rss" href="{{ site.subscribe_rss }}" title="subscribe via RSS">
                        <span class="visible-xs">RSS</span>
                        <img class="hidden-xs" src="{{ root_url }}/images/rss.png" alt="RSS">
                    </a>
                </li>
                {% if site.subscribe_email %}
                <li>
                    <a class="subscribe-email" href="{{ site.subscribe_email }}" title="subscribe via email">
                        <span class="visible-xs">Email</span>
                        <img class="hidden-xs" src="{{ root_url }}/images/email.png" alt="Email">
                    </a>
                </li>
                {% endif %}
            </ul>
            {% if site.simple_search %}
                <form class="search navbar-form navbar-right" action="{{ site.simple_search }}" method="GET">
                    <input type="hidden" name="q" value="site:{{ site.url | shorthand_url }}">
                    <div class="form-group">
                        <input class="form-control" type="text" name="q" placeholder="Search">
                    </div>
                </form>
            {% endif %}
        </div>
    </div>
</nav>
{% endraw %}
{% endcodeblock %}


`1px`の齟齬を解消するには､`max-height: 50px;`を設定します｡メニューバーのタイトル部分の項目は、`.navbar-default .navbar-brand`で設定します｡


``` css sass/partials/_header.scss
header[role=banner] {
    /* fix email / rss icon for bootstrap navbar */
    .navbar-default .navbar-nav > li img {
        height: 18px;
    }
}

.navbar {
margin-bottom: 40px;
border: 0;
}

.navbar-default {
background-color: #E4E4E4;
background-image: none;
background-repeat: none;
border-radius: 0px;
-webkit-box-shadow: none;
box-shadow: none;
}

.navbar-default .navbar-nav>.active>a {
max-height: 50px;
color: #000;
background-image: -webkit-linear-gradient(top,#428bca 0,#428bca 100%);
background-image: linear-gradient(to bottom,#428bca 0,#428bca 100%);
  -webkit-box-shadow: none;
  box-shadow: none;
}

.navbar-nav > li:hover {
max-height: 50px;
background-image: -webkit-linear-gradient(top,#428bca 0,#428bca 100%);
background-image: linear-gradient(to bottom,#428bca 0,#428bca 100%);
}

.navbar-default .navbar-brand {
color: #428bca;
}

.navbar-nav > .active:hover {
max-height: 50px;
opacity: 0.5;
background-image: -webkit-linear-gradient(top,#428bca 0,#428bca 100%);
background-image: linear-gradient(to bottom,#428bca 0,#428bca 100%);
}

.container2 {
  text-align: center;
  font-size: 29px;
  font-weight: 100;
  color: #428bca;
  background-color: #000000;
}

.container2 img:hover {
  opacity: 0.4;
  transition: 0.7s;
}
```

###Menubar ver.3

メニューを選択した時に、境界をはっきりできるようにしました。

``` css sass/partials/_header.scss
.navbar-nav>li{
border-right: solid 1px #e7e7e7;
}
```


##<a name="page10">スライド式の「続きを読む」</a>

マウスオーバーすると､こんな感じでスライドします｡iPhoneの「スライドでロック解除」みたいなイメージです｡



テーマは、`octostrap3`を使っているので、注意してください｡


以下のようなファイルを作り、指定の場所に置きます｡


``` css sass/custom/_more
.btn {
  width: 100%;
  height: 40px;
  padding: 9px 20px;
  border-radius: 0px;
}

.btn:hover,
.btn:focus {
  border-color: #535353;
  border-right: solid 40px #535353;
  color: #fff;
  transition: 0.7s;
  background-color: #99CCFF;
  padding-left: 80%;
  border-left: solid 1px #535353;
}

.btn-default {
  border-color: #404040;
  border-left: solid 40px #404040;
  text-align:left;
  box-shadow: none;
    -webkit-box-shadow: none;
  text-shadow: none;
  background-image: none;
  background-color: #428bca;
  color: #fff;
}

.btn-default a {
  background-color: #428bca;
}
```

そして、`sass/_base.scss`に以下を追記します｡


{% codeblock lang:css sass/_base.scss %}
@import "custom/_more.scss";
{% endcodeblock %}

##<a name="page11">コメントフォーム、Disqus</a>

[Disqus](http://disqus.com/)というのは、非常に有名なコメントサービスのことです｡


`Disqus`には、日本語はないみたいですが､デフォルトでもそれなりの外観と使いやすさを持っているため、多くのブログに広く使われています｡


###Disqusの設置

`Disqus`を設置する方法は、[サイト登録](http://disqus.com/admin/create/)にて、サイトを登録して、[設置コード](http://disqus.com/admin/settings/install/)を取得します。


それをブログに設置すれば､多くのブログに使用できます｡


通常は､以下の様なコードになっています｡

``` html disqus_thread  http://disqus.com/ Link
<div id="disqus_thread"></div>
    <script type="text/javascript">
        /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
        var disqus_shortname = 'ここに入る名前がショートネームです'; // required: replace example with your forum shortname

        /* * * DON'T EDIT BELOW THIS LINE * * */
        (function() {
            var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
            dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
            (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
        })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    <a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
```

####OctopressでのDisqusの設置

まず、`shortname`の取得を具体的に説明します｡






次に､`octopress/_config.yml`を以下のように編集します｡


``` css octopress/_config.yml
    # Disqus Comments
    disqus_short_name: shortname
    disqus_show_comment_count: true
```




なお、設定ファイルである`_config.yml`を書き換えても`rake preview`は効かないので注意してください｡


####OctopressでDisqusを設置した理由

サイトが遅くなるので､あまり設置したくなかったのですが､設置してみました｡


OctopressにDisqusを設置した理由としては､記事下の境界を分かりやすくするためです｡


最初は､`border`でも使おうと思ったのですが､この際、コメントを設置したほうが一石二鳥だと思いました｡


なんかあれば､すぐに外しますが､今のところこんな感じです。


##<a name="page12">文章幅の調整</a>

###行間の幅の調整

行間を調整するには､`line-height`を使います｡


{% codeblock lang:css %}
body {
line-height: 150%;
}

p {
line-height: 200%;
}
{% endcodeblock %}


###改行の幅の調整

私の場合は､`br`要素を変更するのではなく､`p`要素を変更することで対応しました｡

{% codeblock lang:css %}
p {
margin-bottom: 30px;
}
{% endcodeblock %}

###見出しの調整

少しだけ見出しの下が窮屈だったので､調整してみました｡

{% codeblock lang:css %}
h2 {
margin-bottom: 40px;
}
{% endcodeblock %}

##<a name="page13">Octostrap3のPager</a>

アイコンの形を変えたり､表示場所を変えたり､記事タイトルを消したりしました｡





一応､モバイルサイトを考慮した結果です｡


Octostrap3のPagerは、`source/index.html`と`source/_layouts/post.html`でカスタマイズできます。


CSSの方は､`source/assets/bootstrap/dist/css/bootstrap.css`を参考に、カスタマイズしていきましょう。


###Octostrap3のPagerの角丸を削除する

[GitHub Pages + Octopress カスタマイズ](http://qiita.com/PSP_T/items/07365ed24eef63602233)に書きました｡


具体的には､`.pager li &gt; span`を変更します｡


``` css sass/custom/_styles.scss http://octopress.org/docs/blogging/code/ Link
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 10px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
}
```


###Octostrap3のPagerを一番下に表示する

`Disqus`よりも下に表示したほうが良いと思いました｡


記事にコメントが書き込まれた場合､一つの情報として見ることができるからです｡

{% codeblock lang:html source/_layouts/post.html %}
{% raw %}
{% if site.disqus_short_name and page.comments == true %}
     <section>
       <h1>Comments</h1>
       <div id="disqus_thread" aria-live="polite">{% include post/disqus_thread.html %}</div>
     </section>
{% endif %}

{% if page.previous.url or page.next.url %}
  <ul class="meta text-muted pager">
    {% if page.previous.url %}
    <li class="previous"><a href="{{page.previous.url}}" title="Previous Post: {{page.previous.title}}">&larr;&nbsp;Older</a></li>
    {% endif %}
    {% if page.next.url %}
    <li class="next"><a href="{{page.next.url}}" title="Next Post: {{page.next.title}}">Newer&nbsp;&rarr;</a></li>
    {% endif %}
  </ul>
{% endif %}
{% endraw %}
{% endcodeblock %}

上がコメントで下がページャーです。

###Octostrap3のPagerにタイトルを入れない

上のコードでタイトルを入れない処理は完成していますが、`{{page.next.title}}</a>`みたいなところを`Newer&nbsp;&rarr;</a>`に書き換えた気がします｡


これでモバイルでもタイトルが長すぎて「次へ」ボタンの見栄えが悪くなることはありませんね。

##<a name="page14">Code Blockの行番号と背景色</a>

色は、黒ベースにしました。背景が白なので、逆の色のほうが見やすいかと思います。

また、行番号も付けました。具体的には、`display: none`が設定されてたみたいです。

####変更前



####変更後



コメントにちょっと気になる表示`XXX`があったのですが、あまり気にしないでおこう...。

``` css sass/partials/_syntax.scss
.highlight .line-numbers, .gist-file .line-numbers {
  //XXX
  //display: none;
  font-family: "Raleway";
  @if $solarized == light {
    background: lighten($base05, 1) $noise-bg !important;
    border-right: 1px solid darken($base07, 2) !important;
    @include box-shadow(lighten($base03, 2) -1px 0 inset);
    //text-shadow: lighten($base02, 2) 0 -1px;
  } @else {
    background: $base02 $noise-bg !important;
    border-right: 1px solid darken($base05, 2) !important;
    @include box-shadow(lighten($base07, 2) -1px 0 inset);
    //text-shadow: darken($base02, 10) 0 -1px;
  }
}

.pre-code {
  background: $base04 $noise-bg !important;
}

.highlight, .gist-highlight {
  background: $base04 $noise-bg;
}

figure.code:not(.panel), .gist {
  .highlight {
          //border-top: 1px solid #ddd;
      }
}

.gist .highlight, figure.code .highlight {
   @if $solarized == light {
     @include selection(adjust-color($base00, $lightness: 23%, $saturation: -65%), $text-shadow: $base00 0 1px);
   } @else {
     @include selection(adjust-color($base06, $lightness: 23%, $saturation: -65%), $text-shadow: $base06 0 1px);
   }
}
```

`sass`の書き方に習って、色を定義しておきます。

``` css sass/base/_solarized.scss
$base04:#191919 !default; //black
$base05:#1A1A1A !default; //black
$base06:#999 !default; //black
$base07:#000 !default; //black
$base08:#E6E6E6 !default; //white
$base09:#fcfcfc !default; //white
$base10:#F8F8F8 !default; //white
```


あと、ノーマルの文字色がちょっと暗いので、変更。この辺は、テーマ`$solarized == light`でやるのかなと思いましたが、調べるのも面倒です。

``` css sass/partials/_syntax.scss
.pre-code {
  color: $base09 !important;
}
```

##<a name="page15">フォントの大きさ</a>

フォントの大きさを少し変更してみました。

``` css sass/custom/_typography.scss
/* 本文 */
.entry-content {
    font-size: 18px;
    @media only screen and (min-width: 768px) {
        font-size: 18px;
    }
```

``` css sass/partials/_syntax.scss
/* コード */
.highlight .line-numbers, .gist-file .line-numbers {
    font-family: "Raleway";
    font-weight: 100;
    font-size: 16px;
}

/* コード、タイトル */
figure.code:not(.panel), .gist {
    figcaption, .gist-file {
        span, a[href*='#file'] {
            font-size: 16px;
            line-height: 1.1;
            //font-weight: 100;
        }
    }
}
```

##<a name="page16">Archiveの変更</a>

基本的に、`source/blog/archives/index.html`と`source/_includes/archive_post.html`をいじればOKです。

設定が細かく分断されていて、非常に分かりにくいんですが...。

以下の様な感じになりました。




##<a name="page18">スラッシュのような線</a>

スラッシュのような線というのは、以下の様な感じのものです。先が細く、真ん中は太いという感じのもの。



`padding-top:10px;`はフォーカスを当てると、上部分が光るようにしているためです。

``` css sass/custom/_styles.scss
.btn {
  width: 100%;
  border: none;
  background: none;
  box-shadow: none;
  padding-bottom: 0;
  padding-top:10px;
}

.btn:before, .btn:after{
display: block;
content: '';
height: 1px;
background-image: -webkit-linear-gradient(left, #fff, #4bccff, #fff);
background-image: -moz-linear-gradient(left, #fff, #4bccff, #fff);
background-image: -ms-linear-gradient(left, #fff, #4bccff, #fff);
background-image: -o-linear-gradient(left, #fff, #4bccff, #fff);
}

.btn:hover,
.btn:focus {
color:#000;
background-image: -webkit-linear-gradient(left, #fff, #5495D6, #fff);
background-image: -moz-linear-gradient(left, #fff, #5495D6, #fff);
background-image: -ms-linear-gradient(left, #fff, #5495D6, #fff);
background-image: -o-linear-gradient(left, #fff, #5495D6, #fff);
transition: 0.7s;
}

.btn-default{
margin:0px;
}
```

しかし、`.btn`辺りの設定が一体どのファイルから変換されてるのか分からない...。


##<a name="page19">codeのカスタマイズ</a>

キーワードを強調する`code`タグをカスタマイズしてみました。



``` css sass/custom/_syntax.sass
code {
word-break: break-all;
white-space: inherit;
background-color: #F5F5F5;
border: 1px solid #DCDCDC;
font-size: 100%;
}

pre code{
border:none;
}
```

そういえば、`font-size`が90%になっているのは、1行でたくさん使った場合に、重ならないようにするためでしたね。

以下、実験です。

###１行でたくさんのcodeを使った場合の表示

`octopress`,`octopress`,`octopress`,`octopress`,`octopress`,`octopress`,`octopress`,`octopress`,`octopress`,


##<a name="page20">Sidebarにいろいろ設置する</a>

###octopress-tagcloud

タグクラウドをサイドバーに表示します｡


https://github.com/tokkonopapa/octopress-tagcloud

```
.
├─ plugins/
│  └── tag_cloud.rb
└─ source/
   └─ _includes/
      └─ custom/
         └─ asides/
            ├─ category_list.html
            └─ tag_cloud.html
octopress/_config.yml
default_asides: [
    asides/recent_posts.html,
    custom/asides/about.html,
    custom/asides/tag_cloud.html
]
```


###octopress-category-list

タグリストをサイバーに表示します｡

https://github.com/ctdk/octopress-category-list

http://kaworu.github.io/octopress/blog/2013/10/03/category-list-aside/

{% codeblock lang:html source/_includes/custom/asides/category_list.html %}
{% raw %}
<section class="panel panel-default">
  <div class="panel-heading">
    <h3 class="panel-title">Categories</h3>
  </div>
  <div class="list-group">
    {% for category in site.categories %}
    {% capture category_url %}{{ site.category_dir }}/{{ category | first | slugize | downcase | replace:' ','-' | append:'/index.html'}}{% endcapture %}
    <a class="list-group-item {% if category_url == page.url %}active{% endif %}" href="{{ root_url | append:'/' | append:category_url }}">
        <span class="badge">{{ category | last | size }}</span>
        {{ category | first }}
      </a>
    {% endfor %}
  </div>
</section>
{% endraw %}
{% endcodeblock %}


``` css octopress/_config.yml
default_asides: [
    asides/recent_posts.html,
    custom/asides/category_list.html
]
```


###Qiita Widget

http://qiita-widget.suin.org/

{% codeblock lang:html source/_includes/custom/asides/qiita.html %}
{% raw %}
<a class="qiita-timeline" href="https://qiita.com/users/{ユーザ名}" data-qiita-username="{ユーザ名}">{ユーザ名}のtips</a>
<script src="//qiita-widget.suin.org/widget.js"></script>
{% endraw %}
{% endcodeblock %}


``` html _config.yml
default_asides: [
    asides/recent_posts.html,
    custom/asides/qiita.html
]
```

###Hatena Widget

http://b.hatena.ne.jp/guide/blogparts

``` css sass/custom/_styles.scss
.hatena-bookmark-widget-body ul {
background-color: transparent !important;
padding: 10px 10px 0px 10px;
}

.hatena-bookmark-widget ul li {
}

.hatena-bookmark-widget-title {
display:none;
}

.hatena-bookmark-widget-footer {
}
```

{% codeblock lang:html source/_includes/custom/asides/hatena.html %}
ここにタグを貼り付ける
{% endcodeblock %}

``` html _config.yml
default_asides: [
    asides/recent_posts.html,
    custom/asides/hatena.html
```

##<a name="page21">Div要素全体にリンクを貼る</a>





{% codeblock lang:html source/index.html %}
{% raw %}
<article class="post" onclick="location.href=&#34;{{ root_url }}{{ post.url }}&#34;;" style="cursor: pointer;">
  {% include article.html %}
</article>
{% endraw %}
{% endcodeblock %}


``` css partials/_blog.sass
article.post:hover {
background-color: #CCFFFF;
opacity: 0.8;
-webkit-transition: 0.3s ease-in-out;
-moz-transition: 0.3s ease-in-out;
-o-transition: 0.3s ease-in-out;
transition: 0.3s ease-in-out;
}
```

##<a name="page22">画像枠を変更する</a>

デフォルトでは、画像枠が大きすぎるので、変更しました。


``` css partials/_blog.sass
img:not(.no-border) {
  border-radius: 0.2em;
  box-shadow: rgba(0,0,0,0.15) 0 1px 3px;
  -webkit-box-shadow: rgba(0,0,0,0.15) 0 1px 3px;
  -moz-box-shadow: rgba(0,0,0,0.15) 0 1px 3px;
  -ms-box-shadow: rgba(0,0,0,0.15) 0 1px 3px;
  -o-box-shadow: rgba(0,0,0,0.15) 0 1px 3px;
  border: #fff 0.3em solid;
  //@include shadow-box;
}
```

##todo
###domain
http://hamasyou.com/blog/2014/03/05/github-pages-custom-domain/
http://blog.awairo.net/blog/2013/12/14/custom-domain-for-gh-pages/

###tags
http://rcmdnk.github.io/blog/2013/04/12/blog-octopress/


##<a name="page23">AppStoreのアプリを紹介する</a>

[sotsy/appbox-octopress · GitHub](https://github.com/sotsy/appbox-octopress)


まず、`octopress`のルートディレクトリにて、必要なものをインストールします。

``` ruby ~/octopress/Gemfile
gem 'nokogiri'
gem 'json'
gem 'appbox-octopress'
```

{% codeblock lang:bash %}
$ bundle install

$ appbox-octopress install
{% endcodeblock %}

{% codeblock lang:bash %}
$ cd ~/octopress/source/stylesheets

$ curl -O https://raw.githubusercontent.com/sotsy/appbox-octopress/master/templates/css/appbox.css

$ cd ~/octopress/plugins

$ curl -O https://raw.githubusercontent.com/sotsy/appbox-octopress/master/templates/plugins/appbox.rb

$ vim ~/octopress/source/_includes/custom/head.html
{% endcodeblock %}

{% codeblock lang:html ~/octopress/source/_includes/custom/head.html %}
{% raw %}
<link href="{{ root_url }}/stylesheets/appbox.css" media="screen, projection" rel="stylesheet" type="text/css">
{% endraw %}
{% endcodeblock %}


以下の様な書き方ができるようになります。

{% codeblock lang:css %}
{% raw %}
{% appbox appstore 722294701 %}

{% appbox googleplay screenshots com.ea.games.nfs13_row %}
{% endraw %}
{% endcodeblock %}


{% appbox appstore 722294701 %}

{% appbox googleplay screenshots com.ea.games.nfs13_row %}


ただし、このままでは、モバイルでの表示に不都合が生じます。したがって、以下の要素などを使って、CSSを変更します。


``` css ~/octopress/source/stylesheets/appbox.css
.apptitle {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.developer {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

はみ出した部分は、非表示し、非表示が存在する場合は、`...`で表示します。


##<a name="page24">Amazonの紹介を簡単にする</a>

https://github.com/longkey1/octopress-amazon-plugin

{% codeblock lang:bash %}
$ cd /path/to/octopress

$ vi Gemfile
gem 'amazon-ecs'
gem 'i18n'

$ bundle install --path vendor/bundle

$ curl -o ~/path/to/octopress/plugins/amazon_tag.rb https://raw.github.com/longkey1/octopress-amazon-plugin/master/amazon_tag.rb
{% endcodeblock %}


{% codeblock lang:css /path/to/octopress/_config.yml %}
# Amazon plugin
amazon_access_key_id: 'your access key id'
amazon_secret_key:    'your secret key'
amazon_associate_tag: 'your associate'
amazon_cache:         false # or true
amazon_cache_dir:     '.amazon-cache'      # default '.amazon-cache'
amazon_country:       'jp'                 # default 'en'
amazon_local:         'ja'                 # default 'en'
{% endcodeblock %}

使い方は、以下の書式で行います。

{% codeblock lang:bash %}
{% raw %}
{% amazon [type] [asin] %}
type: text, small_image, medium_image, large_image, title, detail, image

{% amazon large_image 4873113946 %}
{% amazon detail 4873113946 %}
{% endraw %}
{% endcodeblock %}


##<a name="page17">参考になるブログ</a>
|タイトル|内容|
|--|--|
|[Glide Note - グライドノート](http://blog.glidenote.com/)|非常にカッコいい雰囲気が出ているブログです｡結構古くからあるOctopress+GitHubで構築されたブログで、これは便利と思えるツールが紹介されています。
|[rcmdnk's blog](http://rcmdnk.github.io/)|更新頻度が高く、主に、経験に基づいた情報を配信してくれているブログです｡こういう方向性はすごく好き。かなりカスタマイズされているようで､オリジナル性が高い感じです｡
|[酒と泪とRubyとRailsと](http://morizyun.github.io/)|デフォルトテーマをそのまま使用しているブログです｡内容は非常にしっかりしていて､分かりやすく書かれています。カスタマイズはあまりなされていない感じですが、Octopressのテーマは、私の好みに合致しているので、そのままでも十分に読みやすいです。
|[haya14busa](http://haya14busa.com/)|デザインが非常に素敵なブログ。個人的には、このサイトを参考にデザインを考えていきたいです。
|[SOTA](http://deeeet.com/writing/)|綺麗でシンプルなデザインが特徴的なブログ。一読性とシンプルさが逸材。
|[mimemo](http://www.miukoba.net/)|タイトルのフォントが美しいブログです。最近、タイトルを細字にするの流行ってるみたいですね。テーマをそのまま使っているブログ。
|[About Digital](http://blog.digital-bot.com/)|簡潔にいろいろな技術がまとめられている感じのブログ。
|[それはBooks](http://hamasyou.com/)|独自ドメインも取得し、割としっかりと運営されている感じのブログ。特にサイドバーが美しい。
|[@znz blog](http://blog.n-z.jp/)|Octopressのカスタマイズについての記事も多いブログ
|[そんなこと覚えてない](http://blog.eiel.info/)|日常や活動について書かれているブログ
|[TODESKING](http://www.todesking.com/blog/)|主に制作物などが紹介されているブログ
|[OctoFound](http://octofound.annekjohnson.com/)|個人的には非常に好みなデザイン。Bootstrapを使っているブログ。テーマとしても公開されている。
|[Front-end Web Developer - Stephen Coogan](http://coog.ie/)|Octopressの公開されているテーマの中では、一番すごいデザインだと思います。

