---
layout: post
title: "airjulius.vim、Linuxでも音声通知されるようにしました"
date: 2014-08-31
comments: true
categories: [ editor, terminal, os, music]
tags: [ linux, audio, miku, vocaloid]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Vocaloidを使用<!--more--><br clear="all">

`aplay`を使います。再生するファイルは、`airjulius.vim/audio/`以下に置きました。

{% codeblock lang:vim ~/.vimrc %}
" 音声ガイドを使用する
let g:airjulius_julius_audio_on = 1

" 音声ガイドに使用するコマンドの指定
let g:airjulius_julius_audio_command = "aplay -M -t wav"

" 音声ガイドに使用するファイルの指定 (type:miku)
"let g:airjulius_julius_audio_file_1 = "path/to/filename.wav"
"let g:airjulius_julius_audio_file_2 = "path/to/filename.wav"
"let g:airjulius_julius_audio_file_3 = "path/to/filename.wav"
"let g:airjulius_julius_audio_file_4 = "path/to/filename.wav"

" aplayのミュートを解除するコマンド
"" $ amixer sset Master unmute
{% endcodeblock %}

ミュートの場合、解除しておいてください。

{% codeblock lang:bash %}
$ amixer sset Master unmute
{% endcodeblock %}

この設定をすると、音声入力を確認後、「コマンドを実行します」とミクの声で通知します。

音声操作、音声通知があると、仮想マシン、サブマシンを良い感じに操作できて、ちょっとだけ便利感が増しますね。

しかし、自然な発音作るの難しい...。

