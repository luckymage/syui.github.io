---
layout: post
title: "音声入力システムをバックグラウンドで動かしてみる"
date: 2014-12-12
comments: true
categories: shell
tags: [ zsh, julius ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">しばらくの間、音声入力システムを動かしてみて、使えるかどうか様子を見てみることにしました。<!--more--><br clear="all">

![](http://lh5.ggpht.com/-PNivSEPdWOA/VIobvOCeOxI/AAAAAAAAAJw/rkN-5jJD2P8/s0/yui_system_s.gif)


昨日説明したように`Julius Plugin`を作ります。中身は適当に、よく使いそうなコマンドなどを`strcmp`の条件付きで設定してやればOKです。ちなみに、認識した音声の文字列は、`result_str`に入ってます。ただし、`hoge_。`というように、`。`の前に空白が入ってくるので注意です。(出力をなんでこんな使いにくい形式にするのか...)

{% codeblock lang:c background.c %}
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
    char start[] = "うん 。";
    char stop[] = "いや 。";

    if (result_str != NULL) {
        printf("%s", result_str);
        if (strcmp(result_str, start) == 0) {
            printf("start %s", result_str);
            sprintf(use, "growlnotify --image ~/Pictures/icon/syui.png -m '%s : ユイを起動します' -t 'ユイ・システム'", result_str);
            system(use);
            sprintf(cmd, "~/.vim/bundle/airjulius.vim/t/run-origin.sh");
            system(cmd);
        } else if (strcmp(result_str, stop) == 0) {
            printf("stop %s", result_str);
            sprintf(use, "growlnotify --image ~/Pictures/icon/syui.png -m '%s : ユイを終了します' -t 'ユイ・システム'", result_str);
            system(use);
            sprintf(cmd, "pkill julius");
            system(cmd);
        }
    } else {
        /*
           sprintf(use, "growlnotify --image ~/Pictures/icon/syui.png -m '%s' -t 'コマンドではありません'", result_str);
           system(use);
           */
        printf("null %s", result_str);
    }
}
{% endraw %}
{% endcodeblock %}

私は、昨日遊んだ会話APIのやつを設定しました。パソコンに向かって`うん`としゃべると、通知を使った音声入力での会話が始まります。`いや`で会話終了。しかし、`Julius`は精度が酷すぎて、この言葉すらなかなか読み取ってくれないという所が悲しいです。

あとは、バックグラウンドで起動するスクリプトを実行します。ただし、ここでは、プラグインは別々のフォルダに入れておいてください。つまり、バックグラウンド起動用と会話用の Julius プラグインは別々に置いて、それぞれの起動スクリプトを用意します。

####バックグラウンド起動用

{% codeblock lang:bash run-background.sh %}
{% raw %}
#!/bin/zsh
dir=~/.vim/bundle/airjulius.vim/
#gcc -shared -o background.jpi background.c
${dir}/tool/bin/julius -C ${dir}/tool/main.jconf -C ${dir}/tool/am-gmm.jconf -nostrip  -plugindir ~/julius > /dev/null 2>&1 &
{% endraw %}
{% endcodeblock %}

####会話用

{% codeblock lang:bash run-origin.sh %}
{% raw %}
#!/bin/zsh
dir=${0:a:h}
#gcc -shared -o test.jpi test.c
${dir:h}/tool/bin/julius -C ${dir:h}/tool/main.jconf -C ${dir:h}/tool/am-gmm.jconf -nostrip -quiet -1pass -plugindir $dir > /dev/null 2>&1 &
{% endraw %}
{% endcodeblock %}

起動時に実行するには、`~/.zprofile`などが便利です。

{% codeblock lang:bash ~/.zprofile %}
## julius : ユイ・システム
# うん : 起動
# いや : 終了
~/julius/run-background.sh
{% endcodeblock %}


