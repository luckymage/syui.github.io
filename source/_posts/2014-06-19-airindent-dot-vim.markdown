---
layout: post
title: "airindent.vim"
date: 2014-06-19
comments: true
categories: [terminal, tool, programming]
tags: [editor, vim, indent]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ブログに載せてるコードからも分かるように、インデントはあまりしっかりしてないので、自動化してみました。<!--more--><br clear="all">


##airindent.vim

{% githubrepo syui/airindent.vim %}

このプラグインは、テキスト変更時にインデントを形成します。

仕組みは簡単で、`=G`や`gg=G`を使います。

しかし、`gg=G`の場合は、文頭にカーソル移動してしまいます。

したがって、変換する前の行に再度移動するようにしています。

###install

{% codeblock lang:vim ~/.vimrc %}
NeoBundle "syui/airindent.vim"
{% endcodeblock %}

`:NeoBundleInstall`

###command

|コマンド|内容
|---|---|
|:AirIndentMoveLine|すべての範囲をインデントして戻る
|:AirAutoIndentAllStart|自動ですべての範囲をインデントを開始
|:AirAutoIndentAllStop|自動インデントの停止

###setting

モードの設定があります。`1`で有効にします。

{% codeblock lang:vim ~/.vimrc %}
{% raw %}
" setting {{{
" インデントの自動化を有効にする
let g:air_auto_indent = 1
" 全範囲を対象にしたインデントのキーバインドを設定する
nm <Leader>- <Plug>(AirIndentMoveLine)
" }}}
{% endraw %}
{% endcodeblock %}

###code

####インデント後に直前の行に戻る

{% codeblock lang:vim ~/.vim/bundle/airindent.vim/plugin/airindent.vim %}
fu! s:air_indent_move_line()
  "let cline = getline(v:lnum)
  let air_cmove = line(".") . "G"
  exe ":normal gg=G"
  exe ":normal " . air_cmove
endf
{% endcodeblock %}

文字列として現在行とコマンドを保存します。

そして、保存したコマンド文字列を`exe`によって実行します。

####上のコマンドを自動化する

{% codeblock lang:vim ~/.vim/bundle/airindent.vim/plugin/airindent.vim %}
fu! s:air_auto_indent_start()
  aug vimrc_air_indent
    au!
    au BufReadPost,BufUnload * call <SID>air_indent_move_line()
  aug END
endf
{% endcodeblock %}

`BufReadPost,BufUnload`によりバッファを開いた時、終了した時に全範囲のインデントを整え、直前の行に戻るコマンドを実行します。


