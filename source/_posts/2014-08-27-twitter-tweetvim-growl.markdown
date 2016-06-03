---
layout: post
title: "TwitterのリストをGrowlに流す"
date: 2014-08-27
comments: true
categories: [ os, editor ]
tags: [ sns, twitter, vim, mac ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ほとんどコードの流用ですが。<!--more--><br clear="all">

##tweetvim_notfiy

[TweetVim](https://github.com/basyura/TweetVim)の最新のツイートを文字列比較し、違いがあれば、通知します。以前にも似たようなの作ったことありましたが、今回は、`system`と`getline`を使っていますので、ある程度の依存関係が無くなったのとクリップボードを汚しません。

[tweetvim_notfiy](https://github.com/syui/tweetvim_notfiy)

{% codeblock lang:vim ~/.vimrc %}
NeoBundle 'syui/tweetvim_notfiy'
NeoBundle 'gist:rhysd/4201877', {
\   'name': 'tweetvim_update',
\   'script_type': 'plugin'
\}
{% endcodeblock %}

または、

{% codeblock lang:vim ~/.vimrc %}
NeoBundle 'basyura/TweetVim'
NeoBundle 'tyru/open-browser.vim'
NeoBundle 'basyura/twibill.vim'

NeoBundle 'syui/tweetvim_notfiy'
NeoBundle 'gist:rhysd/4201877', {
\   'name': 'tweetvim_update',
\   'script_type': 'plugin'
\}
{% endcodeblock %}

`vim +NeoBundleInstall`

###必要なもの

- [tweetvim_autoupdate.vim](https://gist.github.com/rhysd/4201877)

- [growlnotify](http://growl.info/downloads)

###使い方

基本的には、リストを流していますが、特定のユーザーのツイートを流しても良いですし(そのユーザーの他人とのやりとりも流れる)、色々と応用が効きます。

{% codeblock lang:vim ~/.zshrc %}
function tweetvim-auto(){
  vim -c "TweetVimListStatuses $1" +TweetVimAutoUpdate +TweetVimStartNotify
}
{% endcodeblock %}

定義した`tweetvim-auto`コマンドは、リスト名を引数で渡します。

リツイート増えても、通知されるので、注意です。

###コード

一応、小さめにしたコードを表示しておきます。

{% codeblock lang:vim tweetvim_notfiy.vim https://github.com/syui/tweetvim_notfiy/blob/master/plugin/tweetvim_notfiy.vim LINK %}
{% raw %}
let s:tweetvim_notfiy_update_interval_seconds = 2
let s:tweetvim_notfiy_timestamp = reltime()[0]
let s:tweetvim_notfiy_getline_1 = getline(3)

fu! s:tweetvim_notfiy()
  let n_current = reltime()[0]
    if n_current - s:tweetvim_notfiy_timestamp > s:tweetvim_notfiy_update_interval_seconds
        if s:tweetvim_notfiy_getline_1 != getline(3)
          let s:tweetvim_notfiy_getline_1 = getline(3)
          call system("growlnotify -m '" . getline(3) . "'")
        end
        let s:tweetvim_notfiy_timestamp = n_current
    end
endf

fu! s:tweetvim_notfiy_setup_autoupdate()
    aug vimrc-tweetvim-notfiy-autoupdate
        au!
        au CursorHold * call <SID>tweetvim_notfiy()
    aug END
endf

com! -nargs=0 TweetVimStartNotify call <SID>tweetvim_notfiy_setup_autoupdate()
com! -nargs=0 TweetVimStopNotfiy au! vimrc-tweetvim-notfiy-autoupdate
{% endraw %}
{% endcodeblock %}

###設定

{% codeblock lang:vim ~/.vim/bundle/tweetvim_update/plugin/tweetvim_autoupdate.vim %}
let s:tweetvim_update_interval_seconds = 10
{% endcodeblock %}

{% codeblock lang:vim ~/.vim/bundle/tweetvim_notfiy/plugin/tweetvim_notfiy.vim %}
let s:tweetvim_notfiy_update_interval_seconds = 5
{% endcodeblock %}


###テスト

試していませんが。WindowsとLinuxの場合は、こんな感じで通知できそうです。

{% codeblock lang:vim ostype %}
fu! s:air_test_ostype()
let OSTYPE = substitute(system('uname'), "\n", "", "")
if OSTYPE == "Darwin"
  echo OSTYPE
elsei OSTYPE == "Linux"
  echo OSTYPE
elsei has('win32') || has('win16') || OSTYPE =~ "CYGWIN"
  echo OSTYPE
en
endf
com! -nargs=0 AirTestOstype call <SID>air_test_ostype()
{% endcodeblock %}

アイコンです。

{% codeblock lang:vim system %}
let s:air_test_dir_icon= expand("<sfile>:p:h:h") . "/icon/twitter.png"
fu! s:air_test_system()
  call system("growlnotify -a Twitter -m '" . s:air_test_dir_icon . "/test'")
endf
com! -nargs=0 AirTestSystem call <SID>air_test_system()
{% endcodeblock %}

##おまけ:通知

私の場合は、以下のコマンドでTwitterアプリを最小化起動しています。こうすることで、メンションなどが来た場合、通知されます。つまり、公式アプリの通知機能を使っているということです。

{% codeblock lang:bash %}
$ osascript -e 'tell application "Twitter" to close window 1'
{% endcodeblock %}

Macの起動時にコマンドを叩くには、以下のエディタでアプリケーション形式で保存し、アプリを起動時登録しておくとよいでしょう。保存する内容は、`tell application "Twitter" to close window 1`で良いと思います。

{% codeblock lang:bash %}
$ open -a AppleScript\ Editor
{% endcodeblock %}

http://qiita.com/syui/items/b9506d2bf622bed55acc

