---
layout: post
title: "Piapro StudioでWAVのボーカル部分を再現する方法"
date: 2014-08-12
comments: true
categories: [ music ]
tags: [ vocaloid ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">DTM分野、基本的な情報が不足しているような気がするので、初心者には全く分かりません。<!--more--><br clear="all">

##はじめに

音階を1つずつ確認し、入力していくには、時間がかかりすぎます。例えば、「だけど」という言葉を出したいとして、この言葉を自然に出すには、音階がバラバラなのです。

ここで、何かよい方法はないかと探していたら、曲のボーカル部分を抽出し、それを変換、 MIDI を読み込むことで、音階データを Piapro Studio で再現できることが分かりました。

個人的には、これくらい基本的なことは、是非、チュートリアルでも説明しておいて欲しかったです...。

##.mp3から.wavに変換する

`ffmpeg`を使いましょう。

{% codeblock lang:bash %}
$ brew install ffmpeg

$ for i in *.mp3; do ffmpeg -i $i -vn ${i%.mp3}.wav; done
{% endcodeblock %}

後述する`Audacity`を使用する場合は、変換の作業は不要です。ただし、オプション、またはライブラリが必要になるかもしれません。

> Audacityの一番のメリットはWAVファイルだけなく、mp3ファイルも直接編集できるところ！他のソフトはWAVファイルを用意しなくてはいけませんが、Audacityであれば直接mp3を読み込み、編集した音源をWAVでもmp3でも保存することができます。

##.wavからボーカル抽出を行う

[歌声りっぷ](http://www.vector.co.jp/soft/win95/art/se127635.html)でボーカルを抽出するのですが、これには、`.wav(カラオケ)`が必要になります。

ここで、[Audacity](http://audacity.sourceforge.net/download/)でボーカルカットし、`.wav`を作ります。

> メニューより「エフェクト」→「Vocal Remover（for center-panned vocals）」を選択します。

> ボーカルカットをする場合は「Removal choice」を「Remove frequency band」に設定し、下のテキストボックスで周波数を指定しましょう。ボーカル抽出したい音源によりますが、低域は300から500、高域は4000から8000ぐらいの範囲で指定しました。記述方法は「300 8000」というように低域と高域の数値を半角スペースで区切って指定します。



その後、`音声りっぷ`を使って、先ほど作成したファイルと`.wav`を使い、ボーカル抽出を行います。

> おすすめの設定は、「イントロ解析」で「詳細」を指定し、「抽出方法」を「周波数合成」、「音質調整」を「抽出優先」、「抽出レベル」を一番右側（強）の「4.8」にします。その他の設定は標準のままでOKです！

ちなみに、どちらもWindowsソフトなので、Macで動かす場合は、[Wine](http://wiki.winehq.org/FAQ_ja#head-1dde01221cfc22aab3696cc2b2e18c95b412f27f)を使いましょう。

{% codeblock lang:bash %}
$ brew install wine winetricks

$ wine utagoe.exe
{% endcodeblock %}

##.wavから.midに変換する

ボーカル抽出でできたファイル、つまり、`.wav`を使って、音階データを再現します。

[採譜の達人](http://www.pluto.dti.ne.jp/araki/soft/st.html)や[akJ betas](http://sourceforge.jp/projects/akjrcp/releases/#26743)で`.wav`から`.midi`に変換できます。ここでは、`akJ betas`を使います。

{% codeblock lang:bash %}
$ wine st170.exe
{% endcodeblock %}

> 新規, 音声ツール, WavToMidi

<a href="http://www.xucker.jpn.org/product/betas_wav2midi.html" target="_blank">akJBetasでWavをMIDIにする</a>

##.midをPiapro Studioで編集する

後は、作成した音階データを`Piapro Studio`で読み込み、調整していきます。

色々やってみたものの、作曲作業は、やはり、Windowsが一番オススメかもしれません。




##追記

ボーカル抽出は、<a href="http://mahoroba.logical-arts.jp/archives/234" target="_blank">ボーカルキャンセラー2</a>だけで十分でした。


<a href="http://www.h-style.net/dtm-try/%E3%83%9C%E3%83%BC%E3%82%AB%E3%83%AB%E6%8A%BD%E5%87%BA/vocal-pickup-free-3/" target="_blank">簡単ボーカル抽出！フリーソフトでキレイにボーカル抽出できるか試してみた！5本のソフトをレビュー☆その3「ボーカルキャンセラー2」 | ハイレゾスタイル</a>

##参考リンク

<a href="http://yuu0720.blogspot.jp/2014/04/imac.html" target="_blank">ギターとかサイクリングとか: ウチのiMacが、歌った♪</a>

<a href="http://yuu0720.blogspot.jp/2014/04/u.html" target="_blank">ギターとかサイクリングとか: 「U&I」をボカロで歌わせたよ♪</a>

<a href="http://www.h-style.net/dtm-try/%E3%83%9C%E3%83%BC%E3%82%AB%E3%83%AB%E6%8A%BD%E5%87%BA/vocal-pickup-free-4/" target="_blank">簡単ボーカル抽出！フリーソフトでキレイにボーカル抽出できるか試してみた！5本のソフトをレビュー☆その4「歌声りっぷ」 | ハイレゾスタイル</a>

<a href="http://www.h-style.net/dtm-try/%E3%83%9C%E3%83%BC%E3%82%AB%E3%83%AB%E6%8A%BD%E5%87%BA/vocal-pickup-free-2/" target="_blank">簡単ボーカル抽出！フリーソフトでキレイにボーカル抽出できるか試してみた！5本のソフトをレビュー☆その2「Audacity」 | ハイレゾスタイル</a>

<a href="http://ch.nicovideo.jp/my_summer_love/blomaga/ar325083" target="_blank">フリーソフトで作る音MAD（我流）その１:チラシ裏 - ブロマガ</a>

