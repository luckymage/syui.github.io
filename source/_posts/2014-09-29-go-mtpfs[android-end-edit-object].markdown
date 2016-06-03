---
layout: post
title: "go-mtpfs「ANDROID_END_EDIT_OBJECT」とGoogle Backup Transport"
date: 2014-09-29
comments: true
categories: [os, mobile]
tags: android
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">go-mtpfsが上手く動作しなかった<!--more--><br clear="all">

私のAndroidは、通常、ほとんどのアプリを無効化していて、依存関係あたりで、時々、他のアプリの動作に影響を及ぼすことがあります。

今回は、`go-mtpfs`が動かなくなったのですが、`Google Backup Transport`というアプリを無効化したことが原因だったらしいです。エラー表示の出力としては、この辺りのものが表示されていたと思われます。

https://github.com/hanwen/go-mtpfs/blob/master/mtp/android.go#L29

一応、メモしておきます。

ちなみに、`go-mtpfs`は便利なので、使っている人も多いのではないでしょうか。

{% githubrepo hanwen/go-mtpfs %}

