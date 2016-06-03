---
layout: post
title: "vim-gista"
date: 2015-02-25
comments: true
categories: editor
tags: vim
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Gistへのポスト<!--more--><br clear="all">


vim-gistaを使い始めました。

https://github.com/lambdalisue/vim-gista

##インストール

{% codeblock lang:vim ~/.vimrc %}
NeoBundle 'lambdalisue/vim-gista', {
    \ 'depends': [
    \    'Shougo/unite.vim',
    \    'tyru/open-browser.vim',
    \]}
let g:gista#github_user = 'your GitHub user name'
{% endcodeblock %}


##使い方

{% codeblock lang:vim %}
" 初期設定
:Gista --login

" 現在開いているファイルをポスト
:Gista

" 今までポストしたファイルを閲覧、編集
:Gista -l
{% endcodeblock %}

凄く使いやすいです。ありがとうございます。

