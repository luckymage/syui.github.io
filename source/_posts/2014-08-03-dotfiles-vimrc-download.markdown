---
layout: post
title: "dotfilesとvimrcをダウンロード"
date: 2014-08-03
comments: true
categories: [ programming, editor, shell ]
tags: [ dotfile, vim, tool ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">最近、コードリーディングを毎日の日課にしようかなと思って、設定ファイルの整理から始めてみることにしました。<!--more--><br clear="all">

##はじめに

前からできていないことの一つに、私は各種設定ファイルの整理があります。それ故、本設定を未だに公開することもできていないという...。

とにかく、必要な物を追加していって、いらないものをコメントアウトし、問題が起こればその都度対処するという感じで運営しており、...とにかく、酷いんです。なので、人に見せたくないのですよ。

ここで、コードを書けるようになるためには、何よりもまずコードリーディングを習慣化することが重要であり、私もやってみようかなと思っていまして、どうせなら設定ファイルから読んでみようかなと考えました。(最初から興味の薄い所、もしくは難易度を上げ過ぎると挫折の予感がすることもあり

ということで、まずは、コードのダウンロードからやってみることにしました。

##download

スクリプトは、Gistに上げておきました。

###dotfiles

{% codeblock lang:bash dotfilesのダウンロード %}
$ mkdir -p tmp

$ cd !$

$ curl -O https://gist.githubusercontent.com/syui/fd3ea4192b8c61b4b0d1/raw/dotfile_download.sh

$ chmod +x !$:t

$ ./!$
{% endcodeblock %}

###vimrc

{% codeblock lang:bash vimrcのダウンロード %}
$ mkdir -p tmp

$ cd !$

$ curl -O https://gist.githubusercontent.com/syui/b8176fc83d42c105c7f8/raw/vimrc_download.sh

$ chmod +x !$:t

$ ./!$
{% endcodeblock %}

##code

コードは、以下の通りになります。

###dotfiles

{% codeblock lang:bash dotfiles_download.sh %}
{% raw %}
#!/bin/zsh
 
dir=${0:a:h}/dotfiles/
url=`curl https://raw.githubusercontent.com/syui/dotfiles/master/.dotfiles`
line=`echo $url | wc -l | tr -d ' '`
 
for ((i = $line ; i > 0 ; i-- ))
do
  repo=`echo $url | awk "NR==$i"`
  file=`echo $repo | cut -d '/' -f 4`
  file=$dir/$file
  git clone $repo $file
done
{% endraw %}
{% endcodeblock %}

###vimrc

{% codeblock lang:bash vimrc_download.sh %}
{% raw %}
#!/bin/zsh

dir=${0:a:h}"/vimrc"
mkdir -p $dir

# github, bitbucket {{{
dot=`curl http://vim-jp.org/reading-vimrc/json/archives.json | jq -r '.[] | .vimrc | .[] | .url' | sed -e 's/\/github.com/\/raw.githubusercontent.com/g' -e 's/\/blob//g' -e 's/\/gist.github.com/\/gist.githubusercontent.com\/thinca/g' -e 's/\/src/\/raw/g'`

line=`echo $dot | wc -l | tr -d ' '`

for ((i = $line ; i > 0 ; i-- ))
do
  repo=`echo $dot | awk "NR==$i"`
  file=`echo $repo | cut -d '/' -f 4`
  file=$dir/$file
  curl $repo -o $file
done
# github, bitbucket }}}

# gist {{{
dot=`echo $dot | grep "gist.githubusercontent.com" | sed 's/$/\/raw/g'`

line=`echo $dot | wc -l | tr -d ' '`

for ((i = $line ; i > 0 ; i-- ))
do
  repo=`echo $dot | awk "NR==$i"`
  file=`echo $repo | cut -d '/' -f 5`
  file=$dir/$file
  curl $repo -o $file
done
# gist }}}
{% endraw %}
{% endcodeblock %}

