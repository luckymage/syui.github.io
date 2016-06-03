---
layout: post
title: "airjulius.vim"
date: 2014-08-30
comments: true
categories: [ os, editor, terminal ]
tags: [ vim, shell, mac ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">設定をしやすくしました。<!--more--><br clear="all">

[airjulius.vim](https://github.com/syui/airjulius.vim/blob/master/plugin/airjulius.vim)

{% codeblock lang:vim ~/.vimrc %}
{% raw %}
"" Setting {{{
" キーバインド
nm <C-l><C-l> <Plug>(AirJuliusVimShell)
" 通知をONにする
let g:airjulius_julius_growlnotify_on = 1
" 音声ガイドをONにする
let g:airjulius_julius_audio_on = 1
"" }}}

"" 個人設定 {{{
" 音声キーワード
let g:airjulius_julius_sample_word_1 = "こんにちは"
let g:airjulius_julius_sample_word_2 = "テスト"
let g:airjulius_julius_sample_word_3 = "Ｎ"
let g:airjulius_julius_sample_word_4 = "Ｙ"
" 音声入力の実行コマンド
let g:airjulius_julius_sample_command_1 = "osascript -e 'set Volume 1'"
let g:airjulius_julius_sample_command_2 = "open -a 'Google Chrome'"
let g:airjulius_julius_sample_command_3 = "open -a MacVim"
let g:airjulius_julius_sample_command_4 = "open -a iTerm"
" 音声ガイドの実行コマンド
let g:airjulius_julius_sample_audio_1 = "say 音声入力を確認。コマンドを実行しました"
let g:airjulius_julius_sample_audio_2 = "say クロームを起動します"
let g:airjulius_julius_sample_audio_3 = "say ヴイムゥ"
let g:airjulius_julius_sample_audio_4 = "say フォーカスを端末に戻します"
"" }}}
{% endraw %}
{% endcodeblock %}

http://qiita.com/syui/items/c627b04c0f0b878802a9
