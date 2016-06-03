---
layout: post
title: "サイトジェネレーターのHUGOを使ってみた"
date: 2015-01-08
comments: true
categories: blog
tags: golang
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">サブドメイン問題か知らないけど、まだ解決されてなかったみたいな感じでした。<!--more--><br clear="all">


##HUGO

###使い方

[HUGO](http://gohugo.io/)は、ビルドがかなり高速ですが、スクリプトやコマンドが少なく、`push`とか`deploy`とか、そういうのを自分でやりたい人はオススメですが、やりたくない人は、オススメできない感じでした。


{% codeblock lang:bash %}
# install
$ brew install hugo

# template
$ hugo new site my_site

$ cd my_site

# preview
$ hugo server

# build
$ hugo
{% endcodeblock %}

こんな感じで使えます。出来上がったファイル、デフォルトでは、`public`フォルダに置かれますが、それを Web サーバーの方に置けば、作成したページが見れます。

###Theme

テーマのダウンロードは、[個別](https://github.com/spf13/hugoThemes/)にするか、全部するかなど。

{% codeblock lang:bash %}
$ git clone --recursive https://github.com/spf13/hugoThemes.git themes
{% endcodeblock %}

使い方は、大体ドキュメントみれば分かりそうですが、コマンドを叩いて、エラーで確認するとよいでしょう。テーマによって違いますが、そのままで動くの少なかった印象です。

{% codeblock lang:bash %}
{% raw %}
$ git clone https://github.com/roperzh/tinyce-hugo-theme

$ cd !$:t

$ hugo server

$ cat << EOF > config.yaml
---
contentdir: "content"
layoutdir: "layouts"
publishdir: "public"
indexes:
  category: "categories"
baseurl: "http://syui.github.io/hugo-air"
title: "Hugo Blog Template for GitHub Pages"

# https://github.com/spf13/hugo/issues/230
#subdomain: "hugo-air"
#permalinks:
# post: "subdomain/:year/:month/:title/"
EOF

$ mkdir -p theme

$ cp -r layout/{_default,partials} theme/

$ mkdir -p content/posts

$ cat << EOF > !$/newest.md
---
title: "Just another sample post"
date: "2014-03-29"
description: "This should be a more useful description"
categories: 
    - "hugo"
    - "fun"
    - "test"
---
EOF

$ hugo server
{% endraw %}
{% endcodeblock %}

###GitHub Pages

私は、個別記事にサブドメインが変なリンクになって、アクセス出来ないので、`Site.BaseUrl`を`http://syui.github.io/hugo-air`に修正しました。他のファイル(タグやメニュー等)も同じような修正を行わなければならない感じですね。

{% codeblock lang:html layouts/theme/_default/list.html %}
{% raw %}
<div class="post-content">
  <h1 class="post-title">
    <a href="http://syui.github.io{{ .RelPermalink }}">{{ .Title }}</a>
  </h1>

  <span class="post-date">{{ .Date.Format "Mon, Jan 2, 2006" }}</span>

  <p>{{ .Description }}</p>
</div>
{% endraw %}
{% endcodeblock %}

GitHub pagesにポストしたい場合は、[公式通り](http://gohugo.io/tutorials/github_pages_blog/)にやれば良いです。

個人的には、以下のような感じで、リポジトリを作って、`gh-pages`ブランチに`push`します。

{% raw %}
    $ cd public
{% endraw %}

{% codeblock lang:bash gh-pages-push.sh %}
{% raw %}
#!/bin/bash
echo -n username:
read user
repo=`echo $PWD:t`
repo_j={\"name\":\"$repo\"}
url="https://github.com/"$user/$repo.git

curl -u $user https://api.github.com/user/repos -d $repo_j

rm -rf .git

git init

echo $url

git remote add origin $url

git commit --allow-empty -m "noun"

git push -u origin master

git checkout -b gh-pages

git commit --allow-empty -m "noun"

git push -u origin gh-pages
{% endraw %}
{% endcodeblock %}

後は、`push`すればよいです。

{% codeblock lang:bash %}
$ git add *

$ git commit -m "test"

$ git push
{% endcodeblock %}

また、場合によっては、ソースなども`master`に置いておくと良いかもしれません。

ちなみに、`hugo`と`push`は、同時に行えるようにスクリプトを書いておくか、エイリアスでも設定しておくと便利です。

{% codeblock lang:bash deploy.sh %}
#!/bin/bash

cd ~/blog/hugo

hugo

cd public

git add -A

git commit -m "updating a blog `date`"

git push

cd ~/blog/hugo
{% endcodeblock %}

####Demo:

http://syui.github.io/hugo-air/

