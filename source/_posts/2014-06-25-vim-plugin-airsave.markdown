---
layout: post
title: "airsave.vim"
date: 2014-06-25
comments: true
categories: [tool]
tags: [vim, editor, plugin]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Vim の自動保存を実現するプラグインの紹介です。<!--more--><br clear="all">

##airsave.vim

{% githubrepo syui/airsave.vim %}

###install

{% codeblock lang:bash %}
NeoBundle 'syui/airsave.vim'
{% endcodeblock %}

`:NeoBundleInstall`

または、

{% codeblock lang:bash %}
$ curl -o ~/.vim/plugin/airsave.vim https://raw.githubusercontent.com/syui/airsave.vim/master/plugin/airsave.vim
{% endcodeblock %}

###setting

{% codeblock lang:vim ~/.vimrc %}
{% raw %}
" オートセーブを有効にする
let g:air_auto_write = 1
" 書き込みを表示する
let g:air_auto_write_nosilent = 1
" オートセーブを開始する
nm <Leader>s  <Plug>(AirAutoWriteStart)
" オートセーブを停止する
nm <Leader>ss <Plug>(AirAutoWriteStop)
{% endraw %}
{% endcodeblock %}

###code

####airsave.vimの最小構成

`autocmd`を使います。このコマンドを使う場合は、グループ化する必要があります。

{% codeblock lang:vim ~/.vim/bundle/airsave.vim/plugin/airsave.vim %}
aug vimrc_airsave_vim
  au!
  au TextChanged * w
aug END
{% endcodeblock %}

上のコードは、テキストが変更された時`TextChanged`、保存コマンド`:w`を実行するというものです。

####airsave.vimの有効、無効を設定する

{% codeblock lang:vim ~/.vim/bundle/airsave.vim/plugin/airsave.vim %}
{% raw %}
if !exists("g:air_auto_write")
  let g:air_auto_write = 0
en

fu! s:air_auto_write_start()
  "ここにコマンド群を記述
endf

if g:air_auto_write >= 1
  call <SID>air_auto_write_start()
en
{% endraw %}
{% endcodeblock %}

上の処理は、まず、グローバル変数の`g:air_auto_write`が設定されていなければ、`0`を入れます。

そして、最後の行に当該変数が`1`以上ならば定義したコマンド群`function:air_auto_write_start`を実行するというものです。

これにより設定ファイルに`let g:air_auto_write = 1`を書くことにより有効にできます。

