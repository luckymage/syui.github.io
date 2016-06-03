---
layout: post
title: "Vimで文字列をShellScriptの変数に変換するプラグインを作った"
date: 2014-09-07
comments: true
categories: [ editor, shell ]
tags: [ vim, zsh ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">全く役に立ちそうにありませんが、何となく作ってみました。<!--more--><br clear="all">

{% githubrepo syui/airshellcomp.vim %}


{% codeblock lang:vim ~/.vimrc %}
NeoBundle 'syui/airshellcomp.vim'
{% endcodeblock %}

設定は以下の通りです。

{% codeblock lang:vim ~/.vimrc %}
{% raw %}
"" airshellcomp.vim
nm <C-x><C-x> <Plug>(AirShellComp)

" 自動補完を有効にする
let g:airshellcomp_auto = 1
{% endraw %}
{% endcodeblock %}

単語のカーソル下で`C-x, C-x`を押すと、切り替わります。



画面のちらつきが気になる場合は、以下の方法が有効だと思われます。

{% codeblock lang:vim ~/.vimrc http://d.hatena.ne.jp/osyo-manga/20140320/1395327444 LINK %}
{% raw %}
" 処理が表示されないように <silent> でマップする
nnoremap <silent> <Plug>(hoge) :let hoge = 42<CR>
" <silent> で定義したマップを呼び出す
call feedkeys("\<Plug>(hoge)")
{% endraw %}
{% endcodeblock %}

