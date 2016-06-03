---
layout: post
title: "編集しているファイル名を特定の書式で指定行に挿入する Vim script 書いた"
date: 2014-09-13
comments: true
categories: editor
tags: vim
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">最近、Vim script書くようにしていて、Vimスク本を早く読みたい。<!--more--><br clear="all">

{% githubrepo syui/airautofile.vim %}

このプラグイン(単なるスクリプトとも言う)は、`:wq`した時に、ファイル名を特定の書式で指定行(1行目)などに自動挿入するプラグインです。

ほとんど、デフォルトで設定されているので、必要なのは、有効にする設定のみです。

{% codeblock lang:vim ~/.vimrc %}
"" 有効にする
let g:air_autofile_cmd = 1

"" 行の指定
"let g:air_autofile_line = 1

"" 先頭につける文章を指定する
"let g:air_autofile_commnet_h = '#'

"" 書式を指定する
"let g:air_autofile_commnet = '{ file: '

"" 末尾につける文章を指定する
"let g:air_autofile_commnet_f = ' }'
{% endcodeblock %}

コマンドです。

| command | 内容 |
| --- | --- |
| :AirAutoFileStart | 自動ON
| :AirAutoFileStop | 自動OFF
| :AirAutoFileWrite | 手動で挿入
| :let g:air_autofile_line = n | 挿入行の指定

