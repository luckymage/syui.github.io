---
layout: post
title: "Nexus7(2012)をAndroid5.0.2にアップデートしてみた"
date: 2015-01-28
comments: true
categories: mobile
tags: android
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Android 5.0.2<!--more--><br clear="all">

Nexus7をアップデートしてみました。通知がいつまでも来なかったし、何故か公式的な方法ではアップデートできなかったりしたので、rootの場合は来ないのかもしれないけど知りません。

正直、よく分かってないし、調べるもない。色々面倒くさそうで、コマンドを実行している感触で、そんなことを思っています。

そういえば、Dockerの時もそうで、コマンドを実行してる感触で判断して、こんな感じのツールだろうと言いましたが(実は全く調べてなかった)、違ってたみたい。指摘されたことと合わせて考えると、Dockerは、VirtualBoxとは独立してて、Linuxからコンテナを管理するらしいのですが、Macでは、VirtualBoxのLinuxから操作するという感じになってるということかなあ。

さて、本題です。大体の参考は、以下の記事になります。

<a href="http://qiita.com/TEVASAKI/items/2684e096e809cae00860" target="_blank">Android - Nexus7(2012) にLolipop ば入れる！ - Qiita</a>

<a href="http://thjap.org/android/nexus7-2013/6446.html" target="_blank">Android 5.0.2 (LRX22G) Nexus7(2013) に焼く→root まで - 所感 ~android~</a>

##Origin

個人的に実行したコマンド。

####fastboot

[https://github.com/corbindavenport/nexus-tools](https://github.com/corbindavenport/nexus-tools)

{% codeblock lang:bash %}
$ git clone https://github.com/corbindavenport/nexus-tools

$ cp !$:t/bin/*mac /usr/local/bin
{% endcodeblock %}


`install.sh`を実行してもよい。

{% codeblock lang:bash %}
chmod +x install.sh

./install.sh
{% endcodeblock %}


####Android 5.0.2

[https://developers.google.com/android/nexus/images](https://developers.google.com/android/nexus/images)



{% codeblock lang:bash %}
$ aunpack nakasi-factory.tgz 

$ cd `basename !$ .tgz`

$ aunpack image-nakasi-lrx22g.zip 

$ cd `basename !$ .zip`

$ adb reboot bootloader

# fastboot flash boot boot.img
$ mac-fastboot flash boot boot.img

# fastboot erase system
$ mac-fastboot erase system

# fastboot flash system system.img
$ mac-fastboot flash system system.img
{% endcodeblock %}


念の為に、`twrp`と`supersu`はupdateしておきます。

####twrp

[http://techerrata.com/browse/twrp2/grouper](http://techerrata.com/browse/twrp2/grouper) ...2012

[http://techerrata.com/browse/twrp2/flo](http://techerrata.com/browse/twrp2/flo) ...2013

{% codeblock lang:bash %}
# fastboot flash recovery openrecovery-twrp-2.8.4.1-grouper.img
$ mac-fastboot flash recovery openrecovery-twrp-2.8.4.1-grouper.img
{% endcodeblock %}

リカバリモードは`電源`+`-`で起動し、ボタン操作です。

[http://download.chainfire.eu/695/SuperSU/UPDATE-SuperSU-v2.45.zip](http://download.chainfire.eu/695/SuperSU/UPDATE-SuperSU-v2.45.zip)

##所感

面倒くさいの一言。アップデート一つに、ここまでの手間がかかるのは、好きではない。Android SDK Managerを見てると、Androidは、過去の遺物が多すぎて、すごく複雑になってる感じがする。

と言っても、Linux的な雰囲気があるし、慣れれば色々と便利なんだろうな。

そして、なぜかリカバリモードが起動しない感じという。感じというのは、待たされてるし、一瞬画面みたいなものはチラと見えたようなきがするのだけど、やっぱり起動しないので、しばらく通常モード(root制限)で使ってみようと思っています。

ロリポップの感想ですが、良いです。少し動作が重くなったような気がしていますが、画面全体の印象は良いです。エフェクトとかも考えられていて、好きですね。iOSよりも良いです。波とか。時代がやっとPSPに追いついて(ry

rootは、不便があればとりますが、特になければそれほどこだわりはありません。今まで広告なしにするやつに使ってただけという感じなので。

###追記

twrpにおいて、`2012`と`2013`のイメージが間違っていたようで、再度実行したらroot化できました。

##解説

###SDK

[http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html)

{% codeblock lang:bash %}
$ curl -O http://dl.google.com/android/android-sdk_r24.0.2-macosx.zip

$ aunpack !$:t

$ ./`basename !$ .zip`/tools/android
{% endcodeblock %}

`${!$%.*}`とかでは無理だったので、コマンドを使うことに。`android-sdk_r24.0.2-macosx`を取得するために使用します。単なる趣味です。

こういうツールをインストールするのは嫌だなあ...。

###twrp

リカバリモードなど、カスタムAndroidのようなものでしょう。多分。PSPで言うCFW的な。

[http://techerrata.com/browse/twrp2](http://techerrata.com/browse/twrp2)

###supersu

ルート管理アプリ。

[http://download.chainfire.eu/695/SuperSU/UPDATE-SuperSU-v2.45.zip](http://download.chainfire.eu/695/SuperSU/UPDATE-SuperSU-v2.45.zip)

###android-5.0.2

Androidの最新バージョン。

[https://developers.google.com/android/nexus/images](https://developers.google.com/android/nexus/images)

{% codeblock lang:bash %}
$ aunpack nakasi-factory.tgz 

$ cd `basename !$ .tgz`

$ aunpack image-nakasi-lrx22g.zip 

$ cd `basename !$ .zip`
{% endcodeblock %}


ここにある`boot.img`と`system.img`を使うらしいです。

{% codeblock lang:bash %}
$ fastboot flash boot boot.img

$ fastboot erase system

$ fastboot flash system system.img
{% endcodeblock %}


