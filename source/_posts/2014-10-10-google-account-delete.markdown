---
layout: post
title: "アカウントを削除して困ったこと"
date: 2014-10-10
comments: true
categories: private
tags: google
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">アカウントを整理していて困ったことを記録します。<!--more--><br clear="all">

##予備、緊急のアドレスに登録していた場合

削除したメールアドレスを他のWebサービスの予備、緊急のアドレスに登録していた場合、困ったことになりますので、チェックしておいたほうが良いです。

このように、ひとつのサービス、特にメールアドレスを取得できるサービスを使う場合は、他のサービスにも依存関係が生じますので、気をつけなければなりません。

ちなみに、この点は別に困っていませんが、最も注意しなければならないことだと思ったので書きました。

次に書いたことが、個人的に一番痛かったです。

##Picasaのリンクが無効になった

<a href="https://support.google.com/accounts/answer/58582?hl=ja" target="_blank">サービスデータの移行 - Google アカウント ヘルプ</a>

<a href="https://support.google.com/picasa/answer/189356?hl=ja" target="_blank">写真を新しいアカウントに転送する - Picasa と Picasa ウェブ アルバムのヘルプ</a>

> 既存のリンク: 以前のアカウントの既存のリンクや埋め込み画像は以降も動作します。移行が完了すると、新しい場所にリダイレクトされます。

上記を読んで、写真のデータを移行をしたのですが、アドレスが変更されたことによって、ブログに貼っていた画像等が表示されなくなってしまいました。

これについては、もしかしたらダメになるかもしれないなと一応の予想はしていたものの、本当にダメになりました。

正直、その辺りの配慮がある可能性のほうが高いだろうと考えていたのですが、ダメになりました。(大切なのことなので二度言いました

それとも、処理が終わるまでにアカウントを削除したことがいけなかったのかもしれませんが、写真は移行出来ているので、これは関係なさそうです。

といっても、リカバリする方法はあります。実は、アカウントを削除してから1ヶ月くらいはデータが残されます。したがって、申し立てとかを行うと、復活する可能性が高いのです。

よって、旧アカウントを復活させれば画像リンクが有効になる可能性は非常に高いと言えます。

しかし、面倒なので、もういいやと思っています。

また、移行前と後のアドレスに一貫性がなく、一括処理もできませんので、それも放置することにした一要因です。

今まで画像関連は、コマンド一つで`Picasa`への一括アップロード、タグの自動取得をしていただけに、他のサービスへの移行はかなり面倒ですが、もしかしたら移行するかもしれません。

しかし、今のところはその予定はないので、性懲りもなく`googlecl`の再設定をしているのでした。

{% codeblock lang:bash %}
sed -i "" 's/hoge/huga' ~/.config/googlecl/config
{% endcodeblock %}

ちなみに、ブログやっている人は、`googlecl`はかなりオススメなのです。

{% codeblock lang:bash %}
$ pip install gdata googlecl

$ google -h

# bloggerへのポスト
$ google help blogger
$ google blogger post --blog "MBA-HACK" --title "${TITLE}" --tags "${TAG}" filename.html

# picasaへのポスト
$ google help picasa
$ google picasa post -n "${folder}" ~/Pictures/*.png && google picasa list "${folder}" --delimiter " " --fields url-direct
{% endcodeblock %}

