---
layout: post
title: "airchrome.zsh"
date: 2014-06-12
comments: true
categories: [tool, browser, terminal, programming]
tags: [shell, shellscript, applescript, mac, git, chrome, zsh]
---


<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">airchrome.zshのコードを解説します。<!--more--><br clear="all">


https://github.com/syui/airchrome.zsh

##README.md

###features

This article explains the features in `airchrome.zsh`.

`airchrome.zsh` is operates on the Google Chrome from zsh.

`airchrome.zsh` is will only support Mac, And some functions only support of iTerm terminal.

###japanese

この記事は、`airchrome.zsh`の機能について解説します。

`airchrome.zsh`は、 zsh から Google Chrome を操作します。

`airchrome.zsh`は、 Mac のみに対応しています。そして、一部機能は、端末の iTerm を使用します。

###install

{% codeblock lang:bash %}
{% raw %}
$ git clone https://github.com/syui/airchrome.zsh

$ cd !$:t

$ touch ~/.zshrc

$ echo "source $PWD/airchrome.zsh" >> ~/.zshrc

$ source ~/.zshrc
{% endraw %}
{% endcodeblock %}

###bindkey

| key | title
|--|--|
|  ?  | ヘルプ
|  ^e | emacs モードに切り替える
|  ^v | vi モードに切り替える
|  jj | vi の normal モードに切り替える
|  i  | vi の insert モードに切り替える
|  .  | percol のインターフェイスを使う
|  f  | Chrome に f を送る
|  b  | Chrome に特定のキーを送る
|  n  | Chrome に入力を送る
|  0  | ウィンドウを0.0で透過。iTermを使用します。
|  1  | ウィンドウを0.4で透過。iTermを使用します。
|  2  | ウィンドウを1.0で透過。iTermを使用します。
|  j  | スクロール下
|  k  | スクロール上
|  h  | 次へ
|  l  | 前へ
|  w  | タブを閉じる
|  t  | タブの切替
|  o  | タブ
|  r  | リロード
|  p  | ペースト
|  y  | コピー
|  c  | 現在のページにコマンドをコピーします。
|  yu | 現在のページの URL を取得します。
|  yt | 現在のページのタイトルを取得します。
|  yy | 現在のページの URL とタイトルをコピーします。
|  yf | テキストをコピーします。
|  ym | 現在のページの URL とタイトルを Markdown 形式で取得します。
|  yh | 現在のページの URL とタイトルを HTML 形式で取得します。
|  cc | ブログに掲載されているコマンドをコピーします。
|  c; | ブログに掲載されているコマンドを複数行選択コピーします。各コマンドを ; でつなぎます。
|  c@ | ブログに掲載されているコマンドを複数行選択コピーします。各コマンドを && でつなぎます。
|  af | Feedly で自動 RSS URL を開きます。
|  au | Feedly で現在のURL を開きます。
|  ak | airkeepass という外部ツールを開きます。
|  ag | airgoogleplus という外部ツールを開きます。
|  bb | ブックマークを開きます。 percol という外部ツールを使用します。
|  bs | ブックマークのディレクトリ1を選択して、 Chrome で開きます。

##code

`airchrome.zsh`のコードを解説します。

###airchrome.zsh

{% codeblock lang:bash /path/to/airchrome.zsh %}
{% raw %}
# パスの取得
# path {{{
airchrome_dir=$0:h
airchrome_script=$airchrome_dir/script
# path }}}

# デフォルトプロンプトの設定
# prompt {{{
# 現在のバインドモードを取得
EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`

# 現在のバインドモード(文字列)に装飾を施す
EMACS_INSERT="%K{black}%F{034}⮂%k%f%K{034}%F{011} % $EMACS_INSERT %k%f"

# モードが vi の場合の装飾
VIM_INSERT="%K{034}%F{075}⮂%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}⮂%k%f"

# プロンプトの設定
RPROMPT="$EMACS_INSERT$VIM_INSERT"

# キーバインドが emacs モードだった場合のプロンプトの設定
function zle-keymap-select {
    EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`
    if echo $EMACS_INSERT | grep emacs > /dev/null 2>&1;then
        EMACS_INSERT="%K{black}%F{011}⮂%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
        VIM_NORMAL="%K{011}%F{125}⮂%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}⮂%k%f"
        VIM_INSERT="%K{011}%F{075}⮂%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}⮂%k%f"
    else
        EMACS_INSERT="%K{black}%F{034}⮂%k%f%K{034}%F{011} % $EMACS_INSERT %k%f"
        VIM_NORMAL="%K{034}%F{125}⮂%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}⮂%k%f"
        VIM_INSERT="%K{034}%F{075}⮂%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}⮂%k%f"
    fi
    RPROMPT="$EMACS_INSERT${${KEYMAP/vicmd/$VIM_NORMAL}/(main|viins)/$VIM_INSERT}"
    zle reset-prompt
}
zle -N zle-keymap-select
# prompt }}}

# キーバインド emacs モードにした時のプロンプト
# prompt-bindkey {{{
function airchrome-bindmode-emacs () {

    # emacs モードへの切り替え
    bindkey -e

    EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`
    if echo $EMACS_INSERT | grep emacs > /dev/null 2>&1;then
        EMACS_INSERT="%K{black}%F{011}⮂%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
        VIM_NORMAL="%K{011}%F{125}⮂%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}⮂%k%f"
        VIM_INSERT="%K{011}%F{075}⮂%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}⮂%k%f"
    else
        EMACS_INSERT="%K{black}%F{034}⮂%k%f%K{034}%F{011} % $EMACS_INSERT %k%f"
        VIM_NORMAL="%K{034}%F{125}⮂%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}⮂%k%f"
        VIM_INSERT="%K{034}%F{075}⮂%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}⮂%k%f"
    fi
    RPS1="$EMACS_INSERT${${KEYMAP/vicmd/$VIM_NORMAL}/(main|viins)/$VIM_INSERT}"
    RPS2=$RPS1
    zle reset-prompt
}
zle -N airchrome-bindmode-emacs

# vi モードで Ctrl+e を押すと、 emacs モードに切り替えと同時に、プロンプトが設定される
bindkey -v '^e' airchrome-bindmode-emacs

# vi の normal モードで Ctrl+e を押すと、 emacs モードに切り替わると同時に、プロンプトが設定される
bindkey -a '^e' airchrome-bindmode-emacs


function airchrome-bindmode-vi () {

    bindkey -v

    EMACS_INSERT=`bindkey -lL main | cut -d ' ' -f 3`
    if echo $EMACS_INSERT | grep emacs > /dev/null 2>&1;then
        EMACS_INSERT="%K{black}%F{011}⮂%k%f%K{011}%F{034} % $EMACS_INSERT %k%f"
        VIM_NORMAL="%K{011}%F{125}⮂%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}⮂%k%f"
        VIM_INSERT="%K{011}%F{075}⮂%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}⮂%k%f"
    else
        EMACS_INSERT="%K{black}%F{034}⮂%k%f%K{034}%F{011} % $EMACS_INSERT %k%f"
        VIM_NORMAL="%K{034}%F{125}⮂%k%f%K{125}%F{015} % NORMAL %k%f%K{125}%F{black}⮂%k%f"
        VIM_INSERT="%K{034}%F{075}⮂%k%f%K{075}%F{026} % INSERT %k%f%K{075}%F{black}⮂%k%f"
    fi
    RPS1="$EMACS_INSERT${${KEYMAP/vicmd/$VIM_NORMAL}/(main|viins)/$VIM_INSERT}"
    RPS2=$RPS1
    zle reset-prompt
}
zle -N airchrome-bindmode-vi

# emacs モードで Ctrl+v を押すと、 vi モードに切り替わると同時に、プロンプトが設定される
bindkey -e '^v' airchrome-bindmode-vi

# デフォルトキーバインドの設定
bindkey -v

# bindkey }}}

# bindkye {{{
## Ctrl+e をおした時のプロンプトでの実行
#bindkey -sv '^e' 'bindkey -e\n'

#bindkey -se '^v' 'bindkey -v\n'
# }}}

# jj を押すと、 vi の normal モードに切り替わる
bindkey -M viins 'jj' vi-cmd-mode

# ヘルプを表示する
function airchrome-browser-help () {
    $airchrome_script/airchrome_help.sh
}
zle -N airchrome-browser-help
bindkey -a '?' airchrome-browser-help
{% endraw %}
{% endcodeblock %}

###path

zsh scriptのパスの取得を解説します。

{% codeblock lang:bash %}
# スクリプトに記述した場合、現在、スクリプトがあるディレクトリパスを取得する
dir=${0:a:h}

# 現在のディレクトリの一つ上のパスを取得する(上の記述とセットで動作する)
lhome=${dir:h}

# dir に依存しない形で取得する場合
lhome=${0:a:h:h}
{% endcodeblock %}


###directory

私が作るツールのディレクトリ構造を解説します。

{% codeblock lang:bash %}
.
├── LICENSE #ライセンス:cc0
│
├── README.md #説明書
│
├── airchrome.zsh #本体:ディレクトリ名
│
├── tool #外部ツール、ダウンロードファイル
│
├── script #スクリプト、実行ファイル
│   │  
│   ├── hoge.sh
│   │  
│   └── huga.sh
│
├── t #テスト
│   │  
│   └── test.sh
│ 
└── txt #テキスト、テーマファイルなど
    │  
    └── theme.txt
{% endcodeblock %}


###function

以下は、zshで使える`function`の一般的な書式です。

{% codeblock lang:bash %}
# コマンドのまとまりを記述、hogeがコマンド名になる
function hoge () {
    echo command
}

# ラインエディタを有効にする。自分が新しいコマンドを作る場合に必要
zle -N hoge

# キーバインドを設定
bindkey '^a' hoge
{% endcodeblock %}


###percol

percolインターフェイスを使用することが多いです。

[percol - コマンドラインでの選択的インターフェイスについて考える - Qiita](http://qiita.com/syui/items/f2fe51d00378210d10b1)


{% codeblock lang:bash ~/airchrome.zsh/script/airchrome_percol.sh %}
{% raw %}
#!/bin/zsh

# テーマファイルを用意し、それを引数にスクリプトを実行する {{{
# テーマファイルのパスを取得
them=$lhome/txt/theme.txt

# percolでテーマを選択、取得する
opt=`cat $them | percol --query="air-" | cut -d ":" -f 1`

# スクリプトを文字列に応じて実行します
case $opt in

    "air-?")
        $scpt/airchrome_help.sh
        ;;

    "air-ag")
        $scpt/airgoogleplus.sh
        ;;

    *)
        exit
        ;;

esac
}}}
{% endraw %}
{% endcodeblock %}

それに、私は、`case`文を好んで使います。


`case`は、以下のように正規表現を使って判断もできます。

{% codeblock lang:bash %}
#!/bin/bash
key=`read key`

case $key in

  y[Y]es|ok)
    echo yes;;

  n[N]o)
    echo no;;

  *)
    exit;;

esac
{% endcodeblock %}

##script

###Shell Script

####基本的な書き方

Apple Scriptのコマンドラインでの実行は、`osascript`コマンドで行います。ただし、引数の処理が面倒なので、ShellScriptで書いています。

{% codeblock lang:bash iterm_transparency_03.sh %}
{% raw %}
#!/bin/bash
osascript << EOF
tell application "iTerm"
    activate
    tell current session of current terminal
      set transparency to $1
    end tell
end tell
EOF
{% endraw %}
{% endcodeblock %}

`EOF`を使うことで、様々な処理ができます。通常は以下の様に使います。

``` bash EOF
cat << EOF > ~/test.txt
  echo test
EOF

cat << EOF | osascript -
tell application "iTerm"
    activate
    tell current session of current terminal
      set transparency to $1
    end tell
end tell
EOF
```

####Google ChromeでFeedlyを開く

{% codeblock lang:bash %}
#!/bin/zsh

# ディレクトリパス
dir=${0:a:h}

# 現在、Google Chromeで開いているURLを取得
url=`$dir/browser_get_url.sh`

# URLのトップアドレスを取得 (hoge, huga=`command`という書き方もできるかも)
urltop=`echo $url | cut -d "/" -f 1-3`
urlhttpno=`echo $url | cut -d "/" -f 3`
#urlhttpno=$urltop

# Feedlyのアドレス
urlfeedly="http://www.feedly.com/home#subscription/feed"

# ブログサービスによって処理を変更する
if echo $urlhttpno | grep "livedoor.jp\|fc2.com\|blogspot.com\|blogspot.jp\|github.io" > /dev/null 2>&1 ; then

    # livedoor
    if echo $urlhttpno | grep "livedoor.jp" > /dev/null 2>&1 ; then
        open -a "Google Chrome" "$urlfeedly/$urltop/index.rdf"
    fi

    # fc2
    if echo $urlhttpno | grep "fc2.com" > /dev/null 2>&1 ; then
        open -a "Google Chrome" "$urlfeedly/$urltop/?xml"
    fi

    # blogger
    if echo $urlhttpno | grep "blogspot.com" > /dev/null 2>&1 ; then
        open -a "Google Chrome" "$urlfeedly/$urltop/feeds/posts/default"
    fi

    if echo $urlhttpno | grep "blogspot.jp" > /dev/null 2>&1 ; then
        open -a "Google Chrome" "$urlfeedly/$urltop/feeds/posts/default"
    fi

    # github pages
    if echo $urlhttpno | grep "github.io" > /dev/null 2>&1 ; then
        open -a "Google Chrome" "$urlfeedly/$urltop/atom.xml"
    fi
else

    # default:+/feed
    open -a "Google Chrome" "$urlfeedly/$urltop/feed"
fi

exit
{% endcodeblock %}


###Apple Script

####Google Chromeのリロード完了を待つ

``` bash chrome_reload_done.sh
#!/bin/zsh

osascript << EOF
tell application "Google Chrome"
   repeat while loading of active tab of window 1
        delay 0.1
   end repeat
   activate
end tell
EOF
```

####Google Chromeの現在開いているタブをリロードする

``` bash chrome_reload_tab.sh
#!/bin/zsh

osascript << EOF
tell application "Google Chrome"
    reload active tab of window 1
end tell
EOF
```

####Google Chromeで現在開いているタブのURLを取得する

``` bash chrome_get_url.sh
#!/bin/zsh

osascript << EOF
tell application "Google Chrome" to get URL of active tab of first window
EOF
```

####Google Chromeで現在開いているタブのタイトルを取得する

``` bash chrome_get_title.sh
#!/bin/zsh

osascript << EOF
tell application "Google Chrome" to get NAME of active tab of first window
EOF
```

####iTermからGoogle Chromeへキーを送る

``` bash chrome_key_iterm.sh
#!/bin/zsh

osascript << EOF
tell application "Google Chrome"
    activate
    tell application "System Events"
        delay 0.3
        keystroke "$1"
        tell application "iTerm"
            activate
        end tell
    end tell
end tell
EOF
```

`keystroke`と`key code`が使えます。

{% codeblock lang:bash %}
keystroke "v" using {command down, option down, shift down}

key code 53 --esc
key code 51 --delete
key code 48 --tab
key code 49 --space
key code 36 --return
{% endcodeblock %}

####Google Chromeのブックマークを開く

``` bash chrome_open_bookmark.sh
#!/bin/zsh

dir=~/Library/Application\ Support/Google/Chrome/Default/Bookmarks

if [ -e $dir ]; then
    name=`cat $dir | jq -r '.roots.bookmark_bar.children[].children[].name' | percol`
    arg=".roots.bookmark_bar.children[].children[] | select(.name == \"$name\" )"
    url=`cat $dir | jq -r $arg | jq -r .url`
    open -a Google\ Chrome "$url"
fi

exit 0
```

####iTermの透過度を設定する

``` bash iterm_set_transparency.sh
#!/bin/zsh

osascript << EOF
tell application "iTerm"
    activate
    tell current session of current terminal
      set transparency to $1
    end tell
end tell
EOF
```

