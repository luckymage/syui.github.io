---
layout: post
title: "音声で操作するやつ、色々と変更した"
date: 2014-08-30
comments: true
categories: os
tags: mac
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">airjulius.vim、自動ダウンロードするようにしたのと、各OSに対応しました。<!--more--><br clear="all">


[airjulius.vim](https://github.com/syui/airjulius.vim)

{% codeblock lang:vim %}
{% raw %}
""" juliusのダウンロード {{{
fu! s:airjulius_download()
let s:air_tool = g:airjulius_julius_dir_juliuskit
let s:air_file = s:air_tool . "/dictation-kit.tgz"
let s:air_url = "'http://sourceforge.jp/frs/redir.php?m=iij&f=%2Fjulius%2F60416%2Fdictation-kit-v4.3.1-"
let s:air_mv = 'mv ' . s:air_tool . '/*/* '  . s:air_tool

if filereadable(expand(s:air_file)) == 0

let OSTYPE = substitute(system('uname'), "\n", "", "")
  if OSTYPE == "Darwin"
    let s:air_com = "wget " . s:air_url . "osx.tgz' -O " . s:air_file
  elsei OSTYPE == "Linux"
    let s:air_com = "wget " . s:air_url . "linux.tgz' -O " . s:air_file
  elsei has('win32') || has('win16') || OSTYPE =~ "CYGWIN"
    let s:air_com = "wget " . s:air_url . "win.zip' -O " . s:air_file
  en
    echo "download..."
    call system(s:air_com)
  if has('win32') || has('win16') || OSTYPE =~ "CYGWIN"
    call system('unzip -o ' . s:air_file . " -d " . s:air_tool)
  else
    call system('tar xzvf ' . s:air_file . " -C " . s:air_tool)
  en
    call system(s:air_mv)
    echo 'done!'
en
endf

com! -nargs=0 AirJuliusDownload call <SID>airjulius_download()
nn <Plug>(AirJuliusDownload) :AirJuliusDownload<CR>
""" }}}
{% endraw %}
{% endcodeblock %}


パス周り、またもやハマりました。久しぶりに Vim script を書くと、いつもハマってる気がします。

Windowsは、一応、Cygwinに対応していますが、それ以外は、微妙というか、多分ダメです。パスの区切りがあれですし。この辺は、`vital.vim`使うのだろうけど、面倒なので、また今度触りたいです。

あと、Vimのコマンドウィンドウでダウンロードの進捗などを表示するの、どうすればいいのだろう。`CmdwinEnter`辺りが関連してそうだけどよく分かりませんでした。`vimproc`とか使うのかな。

