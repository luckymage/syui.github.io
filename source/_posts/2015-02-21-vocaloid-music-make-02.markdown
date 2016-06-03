---
layout: post
title: "ボカロ作曲入門2"
date: 2015-02-21
comments: true
categories: music
tags: vocaloid
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ボカロの作曲入門2です。UTAUだけで作曲してみます。<!--more--><br clear="all">

##はじめに

[前回](http://syui.github.io/blog/2015/02/20/vocaloid-music-make/)の記事では、大まかな作曲手順と方向性を示しました。したがって、今回は、もう少し具体的に、誰でも実行できるような形で作曲入門を書いていきたいと思います。ということで、フリーソフト、ボーカロイドである`UTAU`を使うことになります。

ちなみに、私自身も初心者なので、この記事の信頼性は、それほど高いものではありません。むしろ一緒に勉強していこう程度のものだと考えていただければ幸いです。

私がこのような記事を書く理由は、自分がボカロ曲を作った時、こういったコンセプトの記事、具体的には、「とりあえず初心者が曲を完成させてみる」というコンセプトで書かれた記事があまり見つからず、苦労したためです。

##必要なもの

今回、必要なものを限定して、単純に曲を完成させることだけを目標にしたいと思います。

[UTAU](http://utau2008.xrea.jp/)

UTAUは、ボーカロイド(音源)に歌を歌わせるためのソフトです。ボーカロイドに発音させるには、音源をダウンロードしてこなければなりません。ここで、音源は波音リツがオススメです。ただし、このソフトは、あくまでボーカロイドに歌わせるだけですので、曲を作りたい場合は、UTAUで作った歌とBGMを合成させなければなりません。ちなみに、合成は、Audacityというソフトが便利です。

[波音リツ](http://ritsu73.is-mine.net/voicebank.html)

ボーカロイド音源と呼ばれるもので、いくつかUTAUで使えるフリーの音源が公開されています。波音リツは、その中の一つで、個人的には最もおすすめする音源です。

[連続音一括設定](http://z-server.game.coocan.jp/utau/utautop.html#autoren)

これは、UTAUプラグインです。波音リツには、単独音、連続音、キレの三種類の音源がありますが、連続音とキレを発音させるには、このプラグインで設定する必要があります。

[Audacity](http://audacity.sourceforge.net/?lang=ja)

歌とBGMを合成させるために使えるソフトです。

##作曲手順

###ボーカロイドに歌わせる

まず、[UTAU](http://utau2008.xrea.jp/)を起動します。

そして、以下のMIDIファイルを`UTAU`で読み込み、ボーカロイドに歌わせてみましょう。

ここで、少し歌詞を自分好みに変えてみても面白いかもしれません。できれば変えて欲しいかも。そのほうが自分オリジナルの曲ということもあり、モチベーションが上がると思います。

####MIDIファイルを読み込む

具体的な手順です。

以下のファイルをダウンロードし、`ファイル > インポート`します。

http://syui.github.io/script/umi-3.mid

![](http://lh5.ggpht.com/-r9TBo8GmH74/VOjnLMLUykI/AAAAAAAAAeQ/JfxsqZ7_q7Q/s0/WS000000.jpg)

![](http://lh3.ggpht.com/-yGH9EjxDskc/VOjnHqW4YZI/AAAAAAAAAeA/SEsGJJSUPTk/s0/WS000000.jpg)

次に、ボーカロイドを選択しましょう。ボーカロイドの選択方法は、`プロジェクト > プロジェクトのプロパティ > info`です。今回は、[波音リツ-連続音](http://www.canon-voice.com/normal.html)を選択します。

![](http://lh3.ggpht.com/-xfH8N2a2l2Y/VOjnPo_cClI/AAAAAAAAAeo/Dnj4OHKab9Y/s0/WS000000.jpg)

ちなみに、私の環境下では、`C:\Program Files\UTAU\voice\波音リツ連続音Ver1.5.1`というフォルダ構成になっています。具体的には、`波音リツ`の音源をダウンロードしてきて、ダウンロードしたファイルを解凍し、ここに置くと、選択できるようになるはずです。もし選択できない場合は、リロード(再読み込み)をしてみるとよいかもしれません。

さて、連続音を発音させるには、[連続音一括設定](http://z-server.game.coocan.jp/utau/utautop.html#autoren)というプラグインを実行する必要があります。`ツール > プラグイン > 連続音一括設定`を実行します。この時、`C-a`ですべて範囲指定をしておく必要があります。

![](http://lh5.ggpht.com/-fYBI0nlyjVU/VOjnRTa_lNI/AAAAAAAAAew/JJip-6qfiBc/s0/WS000000.jpg)

ここで、私の環境下では、`C:\Program Files\UTAU\plugins\autoren155`というフォルダ構成になっています。具体的には、ダウンロードしたファイルを解凍し、出てきたフォルダをこのフォルダに置けばよいかと思われます。既にソフトを起動している場合は、リロードも忘れずに。

次に、歌詞の挿入ですね。具体的には、以下の歌詞を一括挿入するわけですが、`Ctrl+A`で全範囲を指定し、上のバーにテキストを入れて、その隣にあるボタンを押すと、挿入が完了します。

> ふかいふかいなみだのうみしずかなひかりをとおいとおいなみだのそらまぶしいひかりをゆらめくはどうこのなみだわあおくみたすあなたにささげるなみのおと

![](http://lh4.ggpht.com/-FwVY9c1aYVs/VOjnOsrBAsI/AAAAAAAAAeg/QdJaBcvSA1M/s0/WS000000.jpg)

後は、再生してみてもよいですが、上手く歌えていれば、それを保存します。`Ctrl+S`を押して、ファイルを保存し、`プロジェクト > wavファイルを生成`します。

![](http://lh6.ggpht.com/-hegz16IoLLk/VOjnUim39lI/AAAAAAAAAe8/6-HcwWISiPI/s0/WS000000.jpg)

###BGMの合成

フリーのBGM素材をダウンロードします。

http://dova-s.jp/bgm/play1102.html

そして、ダウンロードしてきたBGM素材と先ほど作成した歌を合成させましょう。

まず、[Audacity](http://audacity.sourceforge.net/?lang=ja)を起動します。

そして、二つのファイル(歌とBGM)をドラッグアンドドロップし、`ファイル > オーディオの書き出し`です。

![](http://lh4.ggpht.com/-BUMcrQA6Kjk/VOjqbqC5v7I/AAAAAAAAAfI/GiQkloTybZc/s0/WS000000.jpg)

###曲の完成と補足説明

これで、曲は完成です。大体の作曲手順は、理解できたでしょうか。

ここで、最初にUTAUに読み込んでもらった`.mid`ファイルの作成方法ですが、これは、今回使用したBGMを元に作成しました。

具体的には、[Wave Tone](http://www.vector.co.jp/soft/winnt/art/se421780.html)というソフトを使って、自動採譜、テンポを設定。少しの調整を加えてMIDIファイルの完成となります。

###曲の調整

個人的には、`UTAU`にて、以下のような編集を行ったものがこちらになります。

<iframe width="100%" height="166" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/192323994&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false"></iframe>

- `プロジェクト > プロジェクトのプロパティ > 波音リツ-キレ`

- `ツール > プラグイン > 組み込みツール > オートピッチ`

- `ツール > プラグイン > 組み込みツール > 母音結合`

結構、自然っぽく聞こえるようになったような気がしなくもないです。一番重要なのは、曲の調整かもしれません。

##まとめ

つまり、まとめると、初心者は以下の手順で作曲するのがオススメです。

###BGMの用意

- フリー素材のBGMを[YouTube](https://www.youtube.com/audiolibrary/music)や[SOUND AUDITION](http://dova-s.jp/bgm/)からダウンロードする

上級者は、自分でイチからBGMを作っても良いし、細かい素材を組みわせてBGMを作ってみると良いです。

###MIDIの作成

- ダウンロードしたBGMを元に、`Wave Tone`を使って、MIDIファイルを作成する

- `Wave Tone`では、リズムと自動採譜及び、音符のつなぎあわせやパターンを幾つか作成することを目標とする

- パターンは、イントロ、サビを意識し、2つあれば十分だと思われるが、実際に歌詞を当ててみないと良し悪しは判断できないため、3パターンくらいを目標に作ると良いと思われる

ちなみに、このソフトは、WAVファイルしか読み込めなかったと思いますので、MP3ファイルなどの場合は、WAVファイルに変換します。この際、`ffmpeg`というツールが便利です。

###歌の作成

- `Wave Tone`で作ったMIDIファイルを`UTAU`で読み込む

- `UTAU`で`波音リツ`を読み込む

- もし、`波音リツ`で連続音を使う場合は、[連続音一括設定](http://z-server.game.coocan.jp/utau/utautop.html#autoren)プラグインを実行する

- 音符に歌詞を入れて、歌を作る。この際、WAVファイルとして保存する

###歌とBGMの合成

- 作成した歌、WAVファイルと先ほど用意したBGMを`Audacity`を使って合成します。

これで、ひとまず曲の完成です。

しかし、一番重要なのは、むしろここからだと思われます。何度も完成した曲を聴いて、修正を繰り返してみましょう。

