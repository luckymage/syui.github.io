---
layout: post
title: "音声でVimを操作するプラグインを作った"
date: 2014-08-29
comments: true
categories: [ os, terminal ]
tags: [ vim, shell, mac ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">airjulius.vim<!--more--><br clear="all">

##airjulius.vim

###解説

まずは、画像から見てもらったほうが分かりやすいです。キー入力していないのに、様々なコマンドが実行されています。これは、音声によるパソコン操作になります。



トリガーとなる音声(発音)は以下の通りに設定しました。

####こんにちは

> ボリュームの大きさを変更する
>
> osascript -e 'set Volume 1'

####テスト

> MacVimを起動する
>
> open -a MacVim

####N

> ターミナルにフォーカスを戻す
>
> open -a iTerm

####Y

> Chromeを起動する
>
> open -a Google Chrome

###必要なもの

[julius](http://julius.sourceforge.jp/)

[VimShell](https://github.com/craftgear/vimshell/blob/master/doc/vimshell.jax)

[airjulius.vim](https://github.com/syui/airjulius.vim)

{% codeblock lang:vim ~/.vimrc %}
NeoBundle 'Shougo/vimshell.vim'
NeoBundle 'syui/airjulius.vim'
{% endcodeblock %}

LinuxでもWindowsでも多分動作すると思います。ただし、Macのみしか動作確認していませんので、本体コードにある`julius`コマンドの箇所を変更する必要があります。

{% codeblock lang:vim plugin/airjulius.vim %}
{% raw %}
call feedkeys("julius -C `brew --prefix julius-dictation-kit`/share/main.jconf -C `brew --prefix julius-dictation-kit`/share/am-gmm.jconf -quiet -nostrip | awk '/pass1_best/ {print $2}'\<CR>\<Esc>")
{% endraw %}
{% endcodeblock %}

###使い方

`:AirJuliusVimShell`を実行すると、VimShellが起動し、`julius`コマンドが実行されます。

仕組みは簡単で、`julius`コマンドの出力を読み取り、出力内容によって指定したコマンドを実行するというものです。

###設定

設定する箇所は、主に以下の箇所です。

{% codeblock lang:vim plugin/airjulius.vim %}
{% raw %}
""" 1 (ノーマルバージョン)
"" 個人設定1 {{{
" 音声キーワード
if !exists("g:airjulius_julius_sample_word_1")
  let g:airjulius_julius_sample_word_1 = "こんにちは"
en
" 音声入力の実行コマンド
if !exists("g:airjulius_julius_sample_command_1")
  let g:airjulius_julius_sample_command_1 = "osascript -e 'set Volume 1'"
en
" 音声ガイドの実行コマンド
if !exists("g:airjulius_julius_sample_audio_1")
  let g:airjulius_julius_sample_audio_1 = "say 音声入力を確認。コマンドを実行しました"
en
" }}}

" 入力音声と音声キーワードが一致した場合、コマンドを実行する処理 {{{
if getline(s:airjulius_julius_getline_1) == g:airjulius_julius_sample_word_1
  " 音声コマンドと実行コマンドを通知する
  call system("growlnotify --image " . g:airjulius_julius_dir_icon . " -t " . g:airjulius_julius_sample_word_1 . ' -m "' . g:airjulius_julius_sample_command_1 . '"')
  " 音声ガイドを流す
  call system(g:airjulius_julius_sample_audio_1)
  " コマンドの実行
  call system(g:airjulius_julius_sample_command_1)
  " 実行したコマンドは、一応、Vimのコマンドプロンプトに表示する
  echo g:airjulius_julius_sample_command_1
en
" }}}

""" 2 (簡易バージョン)
"" 個人設定2 {{{
if !exists("g:airjulius_julius_sample_word_2")
  let g:airjulius_julius_sample_word_2 = "テスト"
en
if !exists("g:airjulius_julius_sample_command_2")
  let g:airjulius_julius_sample_command_2 = "open -a MacVim"
en

if !exists("g:airjulius_julius_sample_word_3")
  let g:airjulius_julius_sample_word_3 = "Ｙ"
en
if !exists("g:airjulius_julius_sample_command_3")
  let g:airjulius_julius_sample_command_3 = "open -a 'Google Chrome'"
en

if !exists("g:airjulius_julius_sample_word_4")
  let g:airjulius_julius_sample_word_4 = "Ｎ"
en
if !exists("g:airjulius_julius_sample_command_4")
  let g:airjulius_julius_sample_command_4 = "open -a iTerm"
en
"" }}}

" コマンドの実行のみの簡易形態(通知なし、音声ガイドなし) {{{
if getline(s:airjulius_julius_getline_1) == g:airjulius_julius_sample_word_2
  call system(g:airjulius_julius_sample_command_2)
  echo g:airjulius_julius_sample_command_2
en
if getline(s:airjulius_julius_getline_1) == g:airjulius_julius_sample_word_3
  call system(g:airjulius_julius_sample_command_3)
  echo g:airjulius_julius_sample_command_3
en
if getline(s:airjulius_julius_getline_1) == g:airjulius_julius_sample_word_4
  call system(g:airjulius_julius_sample_command_4)
  echo g:airjulius_julius_sample_command_4
en
" }}}
{% endraw %}
{% endcodeblock %}

ノーマルバージョンが良い場合もしくは、通知だけ、音声ガイドだけなど個別に設定したい場合は、`2, 3, 4`などにコマンドを追加します。

{% codeblock lang:vim plugin/airjulius.vim %}
{% raw %}
if getline(s:airjulius_julius_getline_1) == g:airjulius_julius_sample_word_2
  call system(g:airjulius_julius_sample_command_2)
  echo g:airjulius_julius_sample_command_2
  ShellCommand...1
  ShellCommand...2
  VimCommand...1
  VimCommand...2
en
{% endraw %}
{% endcodeblock %}

あと、音声キーワードを増やすことができますが、こちらに関しても、各自追記していく方向で。

###感想

あまり、精度良くないです。辞書を作成し、それを使えば認識率高くなるみたいですが。

あと、`say`の音量を大きくしておけば、ここから音声を読み取って、コマンドを連携実行できそうです。ある程度簡単なやりとりなら作れそう。認識精度悪いのでやりませんが。


