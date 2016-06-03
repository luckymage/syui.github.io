---
layout: post
title: "juliusとsay"
date: 2014-08-28
comments: true
categories: [ os, terminal, shell ]
tags: [ audio, command ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Macで音声コマンドを使ってみた<!--more--><br clear="all">

##julius

`julius`は音声認識コマンドです。音声解析して、結果を出力します。`dictation-kit`を使えばですが。これは、辞書データのようなものです。



###インストール

{% codeblock lang:bash %}
$ brew tap oame/nlp

$ brew install portaudio julius julius-dictation-kit

$ brew link julius
{% endcodeblock %}

###使い方

> 音声認識には『音響モデル』という所謂信号処理部分と『言語モデル』という単語等の辞書データが必要になります。

したがって、`-C`にてモデルを指定して使います。

{% codeblock lang:bash %}
{% raw %}
$ julius \
  -nostrip \
  -quiet \
  -C `brew --prefix julius-dictation-kit`/share/main.jconf \
  -C `brew --prefix julius-dictation-kit`/share/am-gmm.jconf
{% endraw %}
{% endcodeblock %}

https://github.com/oame/homebrew-nlp

###ビルド

ビルドから行う場合は以下の様な手順になります。

####必要なもの

<a href="http://www.portaudio.com/" target="_blank">PortAudio</a>

<a href="http://sourceforge.jp/cvs/view/julius/julius4/" target="_blank">Julius</a>

<a href="http://julius.sourceforge.jp/index.php?q=dictation-kit.html" target="_blank">Juliusディクテーション実行キット</a>

{% codeblock lang:bash %}
{% raw %}
# portaudio
$ brew install portaudio

# julius
$ curl -O http://sourceforge.jp/frs/redir.php?m=iij&f=%2Fjulius%2F60416%2Fdictation-kit-v4.3.1-osx.tgz

$ tar xzf dictation-kit-v4.3.1-osx.tgz

$ cd dictation-kit-v4.3.1-osx

$ ./bin/julius \
  -C main.jconf \
  -C am-dnn.jconf
{% endraw %}
{% endcodeblock %}

参考:

<a href="http://nero.blog.com/2012/11/02/macosx-%E3%80%8C%E9%9F%B3%E5%A3%B0%E8%AA%8D%E8%AD%98%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%B3%E3%80%8Djulius-%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB/" target="_blank">MacOSX 「音声認識エンジン」Julius インストール | 奴隷たる一族</a>

<a href="http://about-digital.ldblog.jp/archives/458338.html" target="_blank">Blog::About::Digital : 音声認識エンジンjuliusをLionで試してみた</a>


##say

`say`は、音声出力コマンドです。

###設定

システム環境設定から色々設定すると、日本語も使えます。



###コマンド

{% codeblock lang:bash %}
$ say -v Kyoko こんにちは

$ say こんにちは
{% endcodeblock %}

