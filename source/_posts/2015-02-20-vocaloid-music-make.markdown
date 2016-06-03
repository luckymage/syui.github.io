---
layout: post
title: "ボカロ作曲入門1"
date: 2015-02-20
comments: true
categories: music
tags: vocaloid
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ボカロ曲の作曲入門を割りと真剣に書きます。一応、これを読めば曲を作れるという程度を目標にします。<!--more--><br clear="all">

##はじめに

私は、今年の1月頃から1日に10分程度を目標に、作曲ソフトであるDTMというものを触り始め、約1ヶ月でなんとか1曲を作り上げ、その後は、1時間で1曲程度を作れるようになりました。ただし、1時間で作った曲のレベルは基本的に酷いです。

しかし、こんなに時間がかかったのも、作曲のための良記事が、なかなか見つからなかったためだと個人的にはそう感じています。

また、作曲入門の本を幾つか立ち読みやらしてみた感じでは、これで本当に作れるようになるのか疑問を覚えるものばかりだったように思います。

なので、作曲についても、またかと言われるほどに独学です。(だって、本読んで、何かを作れるようになった試しがないもん。

しかし、この記事は、私のような独学の初心者に分かりやすいように、と言うか、初心者が作曲できるようになるくらいまでの手順をまとめていきたいと思います。

##必要なもの

###全部無料で作曲する場合

####UTAU

http://utau2008.xrea.jp/

####波音リツ UTAU

http://ritsu73.is-mine.net/

####Domino MIDI

http://takabosoft.com/domino

####Audacity

http://audacity.sourceforge.net/?lang=ja

####Wave Tone

http://www.vector.co.jp/soft/winnt/art/se421780.html

####BGM Download

http://dova-s.jp/bgm/play1102.html

###初音ミクを使う場合

####初音ミクV3, Studio One (￥17,280)

http://www.crypton.co.jp/mp/pages/prod/vocaloid/mikuv3.jsp

####Wave Tone (無料)

http://www.vector.co.jp/soft/winnt/art/se421780.html

####YouTube オーディオライブラリ (無料)

https://www.youtube.com/audiolibrary/music

####BGM Download (無料)

http://dova-s.jp/bgm/play1102.html

##作曲手順

###素材の組み合わせ

正直、初心者が作曲するために必要な情報はそう多くはありません。やり方次第ですが、私は、最初は、部品、素材を組み合わせて作っていくやり方が最も合理的だと考えます。

この点、この記事の説明は、主に部品や素材の組み合わせ方の説明となっていると思います。

しかし、既存の記事や本は、部品の作り方から膨大な説明をしている場合が多く、更に、それが作曲手順ではなく、概要を説明するだけのものが多く、これで初心者が作曲できるようになるとは到底思えませんでした。そういった細かい部分は、興味が出てきた時に読めばいいものであって、取っ掛かりからそういったことを意識させるのは、基本的に、良くないと私は考えています。何よりも、最初は、とりあえず曲を完成させてみることを目標にすべきと思います。

とりあえずの完成を目標にする理由は、全体像を掴めないと、何が必要なのかがわからないと考えるからです。

そして、必要なものは、個々人の能力や道具(ソフト)等によっても変化してくると思います。

したがって、この記事では、素材部品を組み合わせ、とりあえず曲を完成させてみることを目標にします。

なのに、何故かこのようなコンセプトで書かれた記事が全く見当たらなかったため、個人的には相当がっかりしました。

そして、これは、分野ごとに書かれる記事の特徴が全く異なるという印象を受けました。

例えば、作曲関連の情報とプログラミング関連の情報では、その質が大きく異なるように思います。そして、適当なキーワードで検索してみると、その差は歴然です。

さて、前置きはこの辺にして、早速、作曲を行っていきたいと思います。

###BGMのダウンロード

簡単そうな曲から行きます。以下の素材をダウンロードします。

http://dova-s.jp/bgm/play1102.html

ダウンロードしたファイルは、`.wav`に変換します。

{% codeblock lang:bash %}
$ ffmpeg -i 涙の海.mp3 umi.wav
{% endcodeblock %}

###採譜

`wave tone`というソフトをダウンロードし、起動させます。このソフトより、自動採譜や調整を行います。

http://www.vector.co.jp/soft/winnt/art/se421780.html

まず、先ほどダウンロードしたBGMを解析します。パラメーターで重要なのは、音階で、`3-6`あたりが適当だと思われます。

![](http://lh6.ggpht.com/-60NEx3sSTso/VOcb2JIO_sI/AAAAAAAAAbc/jPJPE_KINyk/WS000000.JPG)

次に、`解析 > テンポ解析`にて、テンポを設定します。

![](http://lh5.ggpht.com/-_KqJP4KU4q4/VOcb0pbHRcI/AAAAAAAAAbI/IPAdZhFOeDg/WS000000.JPG)

次に、`解析 > 自動採譜`を行います。

![](http://lh6.ggpht.com/-OCte9hOc218/VOcb1i60a_I/AAAAAAAAAbY/ANC5mjehLLk/WS000000.JPG)

後は、採譜の調整ですね。これは、ボカロが歌うところになりますので、出来る限り、前後の音階でつないでいきます。

![](http://lh5.ggpht.com/-xxvrHG-z72Y/VOcb1ICN4kI/AAAAAAAAAbM/-gwFqM1lKXU/WS000000.JPG)

つないでいくというのは、つまり以下のようなことですね。音がないところを埋める作業です。必要ないときは後で消すほうが楽ですから。歌詞の長短もありますし。

![](http://lh6.ggpht.com/-q_Nno5jypFc/VOcdUBFyZhI/AAAAAAAAAck/NJZTxpVU038/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588.png)

ここで、音階によっては、パターンが違いますよね。そこで、いくつかのパターンで編集していきます。つまり、C3とC4では全然自動採譜されるパターンが違います。

また、同じ所は書かないようにすることも大切です。後でコピーすればいいわけですから。あくまでパターンで考えるようにしていくのがポイントです。イメージで言うと、以下のような感じですね。

![](http://lh3.ggpht.com/-xSI-i59y00Q/VOc5tFQ38SI/AAAAAAAAAds/jNEwxxgmT_A/scv.png)

ちなみに、ピアノの音が小さいと時は、以下の画像のところを下げていきます。

![](http://lh4.ggpht.com/-6wilvevCa-I/VOcb2gO6_XI/AAAAAAAAAbk/CfNstpvCzo4/WS000000.JPG)

ここで、出来上がった採譜は、`ファイル > ノートをMIDIファイルに出力`して保存します。私が作成したファイルは、以下のファイルになります。面倒な方はこれを、DTMで読み込んでも良いです。

http://syui.github.io/script/umi.mid

###DTM

私は、初音ミクV3から始めたユーザーなので、DTMは、同梱されている`Piapro Studio One`を使用しています。

![](http://lh4.ggpht.com/-ge9IYT1iklo/VOcb4rS-9yI/AAAAAAAAAcE/6rwmX8tuDmE/WS000000.png)

したがって、それを元に解説していきますが、他のソフトでも同じです。はじめに、`トラック >トラックを追加`し、そのトラックにダウンロードしたBGMを`ソング > ファイルをインポート`にて読み込みます。

![](http://lh6.ggpht.com/-VoFGHDZUAWM/VOchbFSGisI/AAAAAAAAAc8/ST2lObFT_PU/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

次に、先ほど作成した`mid`ファイルを初音ミクの方で読み込みます。`ファイル > 読み込み > MIDIファイル`

![](http://lh5.ggpht.com/-ZcqZqlG0VBs/VOcb5xOOknI/AAAAAAAAAcM/RJxLwwZmaeg/WS000000.png)

そして、パターンを一つのパターン、音階の場所に合わせます。範囲指定し、上下に持ってくればよいでしょう。ここで、`C-S-↓↑`が便利です。


![](http://lh5.ggpht.com/-2uRxSXl4kbE/VOc5thIr9eI/AAAAAAAAAdo/vJqaUFJFzt4/scv.png)

####テンポの設定

![](http://lh3.ggpht.com/-bojKfbjUMs4/VOchaTpukEI/AAAAAAAAAc4/omMDkCHeUTM/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

ちなみに、上の画像でマークしているループも設定しておくと非常に便利です。`wave tone`でもループは多用します。私はショートカットキーを割り当て、何度か聞きながら打ち込みをしていきます。

初音ミクでテンポを読み込むのは、`ファイル > 読み込む > 拍子とテンポ`から可能です。(他に設定する方法はないのか...)

テンポは曲の早さみたいなものです。

####音が出ない時

ちなみに、音がでない時は、`環境設定 > ソング設定`

![](http://lh5.ggpht.com/-raTbM87Gt58/VOcb3ONVLrI/AAAAAAAAAbw/JfwJxJ0BUdI/WS000000.png)

その後、`出力`にてチェックを入れます。

![](http://lh6.ggpht.com/-cBdZeG8HnuA/VOcb4Eri-cI/AAAAAAAAAb8/kUmDIJJIXxQ/WS000000.png)

####初音ミクが出ない時

右カラムにある`Piapro Studio VSTi(インストウルメント)`をトラック(左カラム)のところにドラッグアンドドロップします。

####歌詞を入れていき

後は、歌詞を入れていきます。設定でどのように入れるか変更可能ですが、私の場合は、一つをダブルクリックし、たくさん入力していきます。

![](http://lh3.ggpht.com/-cvQQeTHAGTo/VOcijnKFSuI/AAAAAAAAAdE/6MNnTo20Y7c/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588.png)

後は何度も聴いて、歌詞、言葉を調整します。

一応、最終的な`mid`を公開しおきます。これに歌詞を載せます。

http://syui.github.io/script/umi-2.mid

> ふかいふかいなみだのうみしずかなひかりをせつないなみのおとあおじろいひかり

ちなみに、歌詞は全範囲指定、ダブルクリックでコピーできます。このファイルを使って、後で`UTAU`リメイクをしてみます。

####曲の保存

曲ができたら、`ソング > ミックスダウンをエクスポート`にて保存します。それを適切な形にして、公開したりすると良いと思われます。

{% codeblock lang:bash %}
$ ffmpeg -i Mixdown.wav umi-feat-miku.mp3 
{% endcodeblock %}

デフォルトでは、`~/Documents/Studio\ One/Songs`以下に保存されます。

<iframe width="100%" height="166" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/192094401&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false"></iframe>

###動画にする

動画編集は、単純に`Windows Live ムービーメーカー`を使用。VirtualBox上で使用するには、2D,3Dなどをオンにしたり、ドライバ3Dをインストールしたら、起動できるようになりました。最初は、要件を満たさないので使えないみたいなことを言われました。

使い方は簡単で、画像をドラッグアンドドロップ後、`ホーム > 音楽の追加`, `プロジェクト > 音楽に合わせる`で保存すると動画ファイルができます。

###UTAUでの作曲

先ほど作成した曲をUTAUでカバーしてみたいと思います。以下、簡潔に説明します。

UTAUに、MIDIファイルをインポート(ファイル > インポート)し、好きな音源を設定。歌詞入力していきます。

http://utau2008.xrea.jp/

音源は、`波音リツ`を使用します。波音リツは、単独音、連続音、キレがあります。連続音とキレを使用するには、[連続音一括設定](http://z-server.game.coocan.jp/utau/utautop.html#autoren)が必要になります。これを`UTAU/plugins`フォルダに置いて、`ツール > プラグイン > 連続音一括設定`から使用可能です。

http://ritsu73.is-mine.net/

音源フォルダは、基本的には、`UTAU/voice`に置いて、`プロジェクト > プロジェクトのプロパティ > info`から設定可能です。

![](http://lh6.ggpht.com/-LgVBdpiJXsw/VOcqczU_zBI/AAAAAAAAAdU/PSMeXgaMOyQ/WS000007.JPG)

さて、`.mid`を読み込んだ後は、必要な設定やプラグインを実行し、歌詞を入れていきましょう。全範囲指定(C-a)で一括で入れられます。

![](http://lh5.ggpht.com/-qHyXtDUcH_o/VOM6l4gu3wI/AAAAAAAAAaI/yUmnCVybz9Q/WS000001.jpg)

それを保存した後は、`プロジェクト > wavファイルを生成`を行います。ちなみに、再生は、範囲指定して再生ボタン。

最後に、歌とBGMの合成です。これは、`Audacity`というソフトを使用します。このソフトで、先ほどUTAUで保存した`.wav`とBGMの`.wav`を読み込み(ドラッグアンドドロップ)、`ファイル > オーディオの書き出し`にて保存します。

http://audacity.sourceforge.net/?lang=ja

これで、一応、カバーの完成です。あと、微調整に調整によって、聞こえは良くなると思われます。

作成したものは、以下になります。確かに、リツ(連続音)で歌っています。

<iframe width="100%" height="166" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/192097493&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false"></iframe>

全部無料で作曲する場合、歌詞を入れていく作業を`UTAU`でやるか`Domino`でやるかということになります。ここで、`Domino`を使用する機会があるわけですが、こちらのほうが直接、UTAUで打ち込むよりも調整しやすいと思われます。

簡単ですが、作曲手順の説明は以上です。

こんな感じで、曲を作っていき、慣れてきたら、素材から作成することにも挑戦していきたいと思います。

