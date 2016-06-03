---
layout: post
title: "AIと会話をしてみたよ"
date: 2014-12-11
comments: true
categories: [ shell, editor ]
tags: [ vim, shell ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">AIというか、文字列を送ると、単純な組み合わせで返事をくれるAPIに過ぎないわけですが、何となく遊んでみました。<!--more--><br clear="all">

今回使ったのは、こちら。最近、流行ってるみたいで。


<a href="https://dev.smt.docomo.ne.jp/?p=docs.api.page&api_docs_id=3" target="_blank">雑談対話 | docomo Developer support | NTTドコモ</a>


リクエストを送ると、返事を返してくれます。ただし、APIを利用するには、`API Key`が必要になるので、使いたい方は、取得しておきましょう。

{% codeblock lang:bash %}
$ curl -s -H "Content-type: application/json" -X POST -d "{ \"utt\": \"こんにちは\", \"context\": \"548968da92614\", \"nickname\": \"光\", \"nickname_y\": \"ヒカリ\", \"sex\": \"女\", \"bloodtype\": \"B\", \"birthdateY\": \"1997\", \"birthdateM\": \"5\", \"birthdateD\": \"30\", \"age\": \"16\", \"constellations\": \"双子座\", \"place\": \"東京\", \"mode\": \"dialog\" }" https://api.apigw.smt.docomo.ne.jp/dialogue/v1/dialogue?APIKEY=xxxxxx
{% endcodeblock %}

結果:

{% raw %}
    {"utt":"ちわ","yomi":"ちわ","mode":"dialog","da":"0","context":"548968da92614"} 
{% endraw %}

こういった`JSON`の出力は、`jq`を使って切り取れます。

{% codeblock lang:bash %}
$ echo '{"utt":"ちわ","yomi":"ちわ","mode":"dialog","da":"0","context":"548968da92614"}' | jq .utt -M -r
ちわ
{% endcodeblock %}

今回は、[julius](http://julius.sourceforge.jp/juliusbook/ja/jcontrol.html)という音声認識システムと通知ツールである[growlnotify](http://growl.info/downloads)を組み合わせることで、それらしい形式にしてみました。あと、プロフィールは、[平沢唯](http://ja.wikipedia.org/wiki/%E3%81%91%E3%81%84%E3%81%8A%E3%82%93!%E3%81%AE%E7%99%BB%E5%A0%B4%E4%BA%BA%E7%89%A9)にしてます。[Twitter](https://twitter.com/h1rasawa_yui_)

![](http://lh4.ggpht.com/-LT37CwBS3nM/VImeAAaaiuI/AAAAAAAAAJc/yeCqyD2BzNw/s0/julius_run.gif)

{% raw %}
    $ brew install portaudio
{% endraw %}

{% codeblock lang:vim ~/.vim/plugin/julius-download.vim %}
{% raw %}
""" juliusのダウンロード {{{
fu! s:airjulius_download()
let s:air_tool = g:airjulius_julius_dir_juliuskit
let s:air_file = s:air_tool . "/dictation-kit.tgz"
let s:air_url = "'http://sourceforge.jp/frs/redir.php?m=iij&f=%2Fjulius%2F60416%2Fdictation-kit-v4.3.1-"
let s:air_mv = 'mv ' . s:air_tool . '/*/* '  . s:air_tool

if filereadable(expand(s:air_file)) == 0

let OSTYPE = substitute(system('uname'), "\n", "", "")
  if OSTYPE == "Darwin"
    let s:air_com = "wget " . s:air_url . "osx.tgz' -O " . s:air_file
  elsei OSTYPE == "Linux"
    let s:air_com = "wget " . s:air_url . "linux.tgz' -O " . s:air_file
  elsei has('win32') || has('win16') || OSTYPE =~ "CYGWIN"
    let s:air_com = "wget " . s:air_url . "win.zip' -O " . s:air_file
  en
    echo "download..."
    call system(s:air_com)
  if has('win32') || has('win16') || OSTYPE =~ "CYGWIN"
    call system('unzip -o ' . s:air_file . " -d " . s:air_tool)
  else
    call system('tar xzvf ' . s:air_file . " -C " . s:air_tool)
  en
    call system(s:air_mv)
    echo 'done!'
en
endf

com! -nargs=0 AirJuliusDownload call <SID>airjulius_download()
nn <Plug>(AirJuliusDownload) :AirJuliusDownload<CR>
""" }}}
{% endraw %}
{% endcodeblock %}

`:AirJuliusDownload`

ちなみに、`Julius Plugin`を作る際に、初めて`C`を書いてみましたが、正直、よく分かってません。

プラグインは、C言語で作ったものをコンパイルして使います。

{% codeblock lang:c test.c %}
{% raw %}
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>
#include <time.h>

int
get_plugin_info(int opcode, char *buf, int buflen)
{
  switch(opcode) {
  case 0:
    strncpy(buf, "simple output plugin", buflen);
    break;
  }
  return 0;
}
void
result_best_str(char *result_str, char *stm)
{
  char use[1024];
  char cmd[1024];
  char key[1024] = "xxxxxxxxxxxxxxxxxxxxxx";
  if (result_str == NULL) {
    printf("[failed]\n");
  } else {
    printf("%s\n", result_str);

    sprintf(use, "growlnotify --image ~/Pictures/icon/syui.png -m '%s'", result_str);
    system(use);

    sprintf(cmd, "curl -s -H \"Content-type: application/json\" -X POST -d \"{ \\\"utt\\\": \\\"%s\\\", \\\"context\\\": \\\"548968da92614\\\", \\\"nickname\\\": \\\"唯\\\", \\\"nickname_y\\\": \\\"平沢唯\\\", \\\"sex\\\": \\\"女\\\", \\\"bloodtype\\\": \\\"O\\\", \\\"birthdateY\\\": \\\"1997\\\", \\\"birthdateM\\\": \\\"11\\\", \\\"birthdateD\\\": \\\"27\\\", \\\"age\\\": \\\"16\\\", \\\"constellations\\\": \\\"射手座\\\", \\\"place\\\": \\\"東京\\\", \\\"mode\\\": \\\"dialog\\\" }\" https://api.apigw.smt.docomo.ne.jp/dialogue/v1/dialogue?APIKEY=%s | jq .utt -M -r | xargs -J i growlnotify -m i --image ~/Pictures/icon/yui.png", result_str, key);

    system(cmd);

  }
}
{% endraw %}
{% endcodeblock %}

こんな感じで書きまして、以下のコマンドを実行して使います。

{% codeblock lang:bash %}
# コンパイル
$ gcc -shared -o test.jpi test.c

# プラグインがあるディレクトリを指定,-plugindir
$ ./bin/julius -C main.jconf -C am-gmm.jconf -nostrip -quiet -1pass -plugindir .
{% endcodeblock %}

ちなみに、他のオプションは好みです。

<a href="http://julius.sourceforge.jp/juliusbook/ja/desc_plugin.html" target="_blank">第11章 プラグイン</a>

前に作った`airjulius.vim`と組み合わせると、いい感じになります。

![](http://lh6.ggpht.com/-Oi5gTCHgMjM/VImeJdszAxI/AAAAAAAAAJg/vpr1DNA97mc/s0/julius_run.gif)

音声で会話モードを起動したり、ストップしたりできますので、つまりは、以下の形態になっています。

{% raw %}
    {Vimから音声で起動} > {Shell Backgroundで会話} > {Vimから音声で会話を終える}
{% endraw %}

一応、以上の形式をアップデートで上げておきました。ちなみに、`:AirJuliusVimShell`を実行すると、自動で`Julius`のダウンロードも開始されるようになっていますので、まあ、場合によっては一発で使えるかもです。あと、ダウンロードは時間かかりますので、2-3分、待ちます。

https://github.com/syui/airjulius.vim

{% raw %}
    NeoBundle 'syui/airjulius.vim'
{% endraw %}

使い方は簡単で、`:AirJuliusVimShell`を実行して、指定した実行音声をパソコンに向かってしゃべるだけ。デフォルトでは、`スタート`、`ストップ`になっていますので。しかし、認識精度が酷すぎるので、私は、`お`、`は`にしています。

{% codeblock lang:vim %}
{% raw %}
" syui/airjulius.vim {{{
let g:airjulius_julius_sample_word_1 = "お"
let g:airjulius_julius_sample_word_2 = "は"
let g:airjulius_julius_sample_audio_1 = "起動コマンドを確認。ユイを起動しました"
let g:airjulius_julius_sample_audio_2 = "終了コマンドを確認。ユイをシャットダウンしました"
" }}}
{% endraw %}
{% endcodeblock %}

なぜ、Vimから起動、終了をやってるのかというと、Shellからでもできるのですが、ShellよりもVimを触ってる時間のほうが長いので、そんな感じです。それに、コントローラーまでもバックグラウンドだと忘れがちですし。かと言って、永続化はしたくない....。

ちなみに、コントローラーであるVimを閉じてしまった場合は、`pkill julius`などで終了するとよいです。

通知ではなく、喋らせることも`say`コマンドとかを使えばできます。


