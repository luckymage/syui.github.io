---
layout: post
title: "MacBookAir"
date: 2014-04-11
comments: true
categories: [os, tips]
tags: [mac, linux, windows, kail, arch, manjaro, mavericks, application, tool]
---


<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">MacBookAirを手に入れてから、だいぶ時間が経ちました。ここで、現在では、どういうふうに使っているのかを設定方法や使用しているツールなどを交えて紹介していきたいと思います。<!--more--><br clear="all">


##目次

番号|OS|バージョン
|---|---|---|
01|Mac|[Mavericks](#page02)
02|Windows|[Windows7](#page03)
03|Linux|[Manjaro Linux](#page04)
04|Linux|[Kail Linux](#page05)
05|Tips|[おまけ](#page06)


##<a name="page01">概要</a>


###Mac | Mavericks

`Mavericks`の設定については、ブログでも何度か紹介してきましたので、割と簡単にいきたいと思います。


主に、使用しているツールを書いていきます。


###Windows | Windows7

私の場合、メインとして`Cygwin`と`PowerShell`を使っています。


`Windows7`は、仮想環境上で動作させています。


アプリのインストールは、`Chocolatey`で行います。


その他、Terminalに`Console Z`を使います。


###Linux | Manjaro Linux

現在、もう一つのMacBookAirには、`Manjaro Linux`を直接インストールしています。


ウィンドウマネージャは、`Awesome`を使っています。


最初は、Macとのデュアルブートしてみたのですが、どうもしっくり来なかったので、Macは消しました。非常に快適です。

XPがサポート終了のニュースが入っていますが、個人的には、Manjaro Linux+Awesomeをおすすめします。このOSは、最小構成で非常にサクサク動作します。また、ウィンドウ操作が快適です。


今回は、個人的に一番おすすめのOSです。設定と使っているアプリなどを紹介します。


###Linux | Kail Linux

主に脆弱性検証のために使えるOSです。


こちらも仮想環境上に作成しています。


###Tips | おまけ

情報が多すぎるため、特筆するものは、ここにまとめます。主に、便利コマンドやワンライナーなど。


##Mac | Mavericks

|Mavericks|
|---|
|[Mavericksで使っているアプリ](#p201)
|[MacBookAirで使ってないけど有効なツール](#p202)
|[Mavericksで使える有料アプリなど](#p203)
|[Command Lineで使用しているツール](#p20x)
|[Mavericksの初期設定](#p204)
|[Mavericksにインストールしたアプリ](#p205)
|[MavericksをVirtualBoxにインストールする](#p206)

###<a name="p201">Mavericksで使っているアプリ</a>

####[MacVim](http://code.google.com/p/macvim-kaoriya/)

高機能なエディタ。ちなみに、TweetVimのアイコンを表示するには、設定にて、`Core Textレンダラを使用する`を外して起動し、再度チェックを入れるといける。エイリアスは以下のように設定。

{% codeblock lang:bash ~/.zshrc %}
alias v='env LANG=ja_JP.UTF-8 /Applications/MacVim.app/Contents/MacOS/Vim "$@"'
{% endcodeblock %}


####[iTerm2](http://www.iterm2.com/)

スタイリッシュなターミナルアプリ。パソコン操作はほとんどこのアプリを介して行う。フォーカスを端末に戻すには、以下のコマンドを実行。

{% codeblock lang:bash %}
$ osascript -e 'tell application "iTerm" to activate'
{% endcodeblock %}

####[Google Chrome](http://www.google.co.jp/chrome/intl/ja/landing_ch.html)

要素の検証機能が逸材のブラウザ。CSSやHTMLを少しでも扱うことがあるなら、これ以外には考えられない。

ちなみに、Google Chromeは、起動オプションを付けることもできます。下記は、特定のURLを開くオプションと、プロセス制限の起動オプション。

{% codeblock lang:bash %}
$ open -a Google\ Chrome http://syui.github.io/

$ open -a Google\ Chrome --args --renderer-process-limit=2
{% endcodeblock %}

####[Google IME](http://www.google.co.jp/ime/index-mac.html)

正確なIME日本語入力。個人的な設定としては、まず半角にすることかな。

####[Growl](http://growl.info/downloads)

通知の設定を行うアプリ。CUI版の`growlnotify`もあります。

{% codeblock lang:bash %}
$ growlnotify -t twitter -m tweet!
{% endcodeblock %}


####[XtraFinder](http://www.trankynam.com/xtrafinder/)

Finderのカスタマイズを行うアプリ。Finderの再起動は以下のコマンドを実行


{% codeblock lang:bash %}
$ killall Finder
{% endcodeblock %}


####[BetterTouchTool](http://blog.boastr.net/)

様々なショートカットを設定できるアプリ。

####[TinkerTool](http://www.bresink.com/osx/TinkerTool.html)

Macの隠し機能を簡単に有効にするアプリ。初期設定の時は一度は使う。

####[VirtualBox](https://www.virtualbox.org/wiki/Downloads)

仮想環境でOSを動作させるためのアプリ。簡単に設定を保存、リセット、再生できる。個人的には、かなりの使用頻度で、仮想OSが自分のメイン環境とも言える。イメージの起動は以下の様な感じ。

``` bash
$ VBoxManage modifyvm ubuntu --vrde on && VBoxManage startvm ubuntu
```

####[Skitch](http://update.skitch.com/skitch.html)

スクリーンショットを保存するアプリ。新しいバージョンよりも前のバージョンのほうが人気があった。

####[Dash](http://kapeli.com/dash)

様々な辞書を呼び出すことができるアプリ。コマンドラインからも呼び出せます。

{% codeblock lang:bash DashをCLIから呼び出す http://qiita.com/yuyuchu3333/items/292e99a521a9653e75fb LINK %}
$ open dash://[word]

$ open dash://'[word1] [word2]'

$ open dash://[language]:[word]
{% endcodeblock %}

####[Alfred](http://www.alfredapp.com/)

こちらも高速な検索と呼び出しを設定できるアプリ。`mdfind`というコマンドもあるが、設定が面倒という方はGUIのこのアプリ。

####[Dropbox](https://www.dropbox.com/)

クラウドデータベースアプリ。企業が管理するサーバーにファイルを保存し、簡単で手軽な認証を提供するサービスのクライアントアプリ。

####[ShiftIt](http://code.google.com/p/shiftit/)

ウィンドウをショートカットキーで操作するためのアプリ。

####[Kobito](http://kobitoapp.com/)

Qiitaに記事を投稿できるエディタ。プレビュー機能も備えている。Qiitaは、Markdownで書けるので人気がある。

####[GIMP](http://www.gimp.org/downloads/)

高機能な画像編集アプリ。無料アプリではこれ一択という人が多い。

####[KeePassX](http://keepass.info/download.html)

フリーのパスワード管理アプリ。

####[ClamXav](http://www.clamxav.com/download.php)

コンピュータウィルスをスキャンするためのアプリ。ただし、デフォルトでは監視を行うものではないので注意。

####[ClipMenu](http://www.clipmenu.com/ja/)

クリップボード履歴をいつでも呼び出せるアプリ。

####[CheatSheet](http://www.cheatsheetapp.com/CheatSheet/)

アプリのキー操作をCheatSheetとしていつでも呼び出せるアプリ。

####[CCleaner](https://itunes.apple.com/jp/app/ccleaner/id499268461?mt=12)

パソコンに保存されている一時ファイルや不要なファイルを一括削除してくれるアプリ。

####[VLC](http://www.videolan.org/vlc/)

定番の動画プレイヤー。インターフェイスに`ncurses`を利用すれば、CUI操作ができる。

``` bash
$ /Applications/VLC.app/Contents/MacOS/VLC
```


####[HandBrake](http://handbrake.fr/)


動画変換アプリ。WindowsやLinuxでもこれ一択で使っています。記述するのを忘れてましたが、コメントにて思い出させてもらいました。ありがとうございます。


####[MPEG Streamclip](http://www.squared5.com/)

動画を編集するアプリ。かなり使いやすいのでおすすめ。


####[XQuartz](http://xquartz.macosforge.org/landing/)

X.Org Server に基づく、OS X 向けの X Window System の実装です。

####[ImageUp](http://software.cockscomb.info/imageup/)

IMEのON/OFFをメニューバーに表示してくれるアプリ。

####[AppCleaner](http://freemacsoft.net/appcleaner/ )

アプリの完全削除を実現するためのアプリ。


###<a name="p202">MacBookAirで使ってないけど有効なツール</a>

####[Gentoo Linux](http://www.gentoo.gr.jp/)

> 最小構成で起動するOS。ソースコードを自身でコンパイルする主義を採用している。そのため、ある程度のスペックを備えたマシンで使うのが好ましいと思われる。

####[Ubuntu Linux](http://www.ubuntu.com/)

> 割りと最新の動向に素早い反応を見せるOSというイメージがある。Linuxの中では人気のOS。動作も比較的安定している。

####[Emacs](http://www.gnu.org/software/emacs/)

> 高機能でカスタマイズ性の高いテキストエディタ。テキストエディタを超える存在。

####[Sublime Text](http://www.sublimetext.com/)

> 操作性と拡張性に優れたタブ切り替え型のテキストエディター。Windows, Linux, Macで使える。

####[Eclipse](https://www.eclipse.org/downloads/)

> IDEであり、IBMによって開発された統合開発環境の一つ。Java開発に好んで使われている印象

####[Coda 2](http://panic.com/jp/coda/)

> これについてはよく知らないのだけど、ブロガーの人はみんなこのアプリを持っているらしい。多分、IDEだと思う。

####[Xcode](https://developer.apple.com/xcode/)

> iOSアプリの作成には必須のIDE。

####[GitHub for Mac](http://mac.github.com/)

> GUIのGitHubクライアント。視覚的に分かりやすい。

####[DashExpander](http://itunes.apple.com/jp/app/dashexpander/id458867049?mt=12)

> 軽量でシンプルなテキストエディタ。

####[TextMate](http://macromates.com/)

> オープンソース化なテキストエディタ。かなり人気がある。

####[Mixins Tutorial](http://mixins.chocolatapp.com/tutorial/)

> 高機能で、軽量。拡張機能を JavaScript + Node.js で書ける。

####[TotalFinder](http://totalfinder.binaryage.com/)

> Finderを拡張するアプリ。定番だけど知らなかった。

####[TotalSpaces2](http://totalspaces.binaryage.com/)

> 仮想デスクトップを使いやすくするための定番アプリ。非常に高機能、シンプルな設計です。

####[TotalTerminal](http://totalterminal.binaryage.com/)

> 拡張性の優れたシンプルなターミナルアプリ。

####[NetBeans](http://ja.netbeans.org/)

> 日本語ドキュメントがしっかりしたIDE。使っている人は、少数派な印象。

####[dolipo](http://drikin.com/2010/11/dolipo.html)

> ネット環境の高速化を図るためのアプリ。

####[TeamViewer](http://www.teamviewer.com/ja/index.aspx)

> 簡単なVLCクライアント。VLCというのは、デスクトップのリモート操作のことで、このアプリは、難しいサーバーの設定などを省いてくれる。

####[AccessMenuBarApps](http://www.ortisoft.de/accessmenubarapps/)

> メニューバーへのアクセス改善してくれるアプリ。

####[Quicksilver](http://qsapp.com/download.php)

> ショートカットを設定するためのアプリ。BetterTouchToolを使う人と好みがわかれる。

####[Evernote](http://www.evernote.com/about/intl/jp/)

> クラウドメモアプリ。様々なOSに対応していて、メモを保存できる。

####[Notational Velocity](http://notational.net/)

> Simplenoteのクライアントアプリ。Simplenoteとは、Evernoteのようなものでクラウドメモ帳。


####[Audacity](http://audacity.sourceforge.net/)

> オーディオ編集, とても高性能なのに無料なので定番, VSTも読み込めて重宝します [LINK](http://qiita.com/syui/items/eb0de8ff93d5714d88aa#comment-3a0f6844476550229537)

####[Asepsis](http://asepsis.binaryage.com/)

> .DS_Storeを作らせないようにする, 無料, TotalFinderには機能として含まれてます [LINK](http://qiita.com/syui/items/eb0de8ff93d5714d88aa#comment-3a0f6844476550229537)

####[CotEditor](http://coteditor.github.io/)

> テキストエディタ, 正規表現検索などの強力な機能もありなお無料, シングルウィンドウで透過度が調節可能, 最近開発が再開されたようです [LINK](http://qiita.com/syui/items/eb0de8ff93d5714d88aa#comment-3a0f6844476550229537)

###<a name="p203">Mavericksで使える有料アプリなど</a>

####[PopClip](https://pilotmoon.com/popclip/)

> テキストを選択したときに、ポップアップでメニューを表示してくれるアプリ。使ってる人多い。

####[MarsEdit](http://www.red-sweater.com/marsedit/)

> ブログエディタであり、各種ブログのプレビューを提供してくれる。

####[1Password](https://agilebits.com/onepassword)

> パスワード管理アプリ。いろいろな連携ができて非常に便利。

####[Vmware Fusion](https://my.vmware.com/web/vmware/info/slug/desktop_end_user_computing/vmware_fusion/6_0)

> 仮想化を支援するためのアプリ。非常に人気があり、完結で分かりやすい。例えば、Mavericksの仮想化でもVirtualBoxでは、苦戦するが、このアプリなら一発らしい。

####[TextExpander](https://smilesoftware.com/TextExpander/index.html)

> 高機能なスニペットアプリ。定形入力を保存しておいて使う。

####[Type2Phone](http://itunes.apple.com/jp/app/type2phone/id472717129?mt=12)

> MacのキーボードをBluetoothキーボードにしてしまおうというアプリ。

####[DisplayLink](http://www.displaylink.com/support/downloads.php)

> iPadをデュアルモニタにするアプリ。

####[Flavours](http://flavours.interacto.net/)

> OS X の全体のアピアランスをワンタッチで切り替えられるテーマチェンジャーアプリ。外見にこだわりを持つ人にはおすすめ。

####[Photoshop](http://www.adobe.com/jp/products/photoshop.html)

> 非常に高機能な画像編集アプリ。高価だが、ブロガーの人はみんな持ってるらしい。

####[Illustrator](http://www.adobe.com/jp/products/illustrator.html)

> こちらも同じく、高機能な画像編集アプリ。イラストを描く人には必須アプリ。

####[HATSUNE MIKU V3](http://www.crypton.co.jp/mp/pages/prod/vocaloid/mikuv3.jsp)

これひとつに曲作りのために必要なアプリがまとめられていて、ボカロ曲を作れる。


####[Coolorus](http://www.coolorus.com/)

> カラーピッカー, 有料ですが価格に見合った使いやすさ, Mac OS用のとPS/Fl用プラグインとがあってプラグインはWinにも対応, まもなく2.0リリースなので今は待つ時期かも [LINK](http://qiita.com/syui/items/eb0de8ff93d5714d88aa#comment-3a0f6844476550229537)

####[Window Magnet](https://itunes.apple.com/jp/app/window-magnet/id441258766)

> メニューバーからのウインドウ切り替え選択など。他、スナップショット。Windows のエアロスナップが好きな人は、Window Magnet を購入すると捗るぞ [LINK](http://b.hatena.ne.jp/shinagaki/20140421#bookmark-191352478)


###<a name="p20x">コマンドラインで使用しているツール</a>

####[jq](http://stedolan.github.io/jq/)

`jq`は、JSONのデータを扱いやすくするためのものです。

``` bash
$ brew install jq

$ echo '{"user":"stedolan", "titles":["JQ Primer",  "More JQ"]}' | jq .titles
```

####[fu](https://github.com/samirahmed/fu)

`fu`は、[commandlinefu.com](http://www.commandlinefu.com/commands/browse)からの検索をかけ、コマンドをコピーするものです。

``` bash
$ git clone git://github.com/samirahmed/fu.git

$ cd fu/

$ sudo make install

$ fu -a git

$ fu -c 1
```

####[pandoc](http://johnmacfarlane.net/pandoc/)

`pacdoc`は、様々なドキュメントを変換するものです。

``` bash
$ brew install haskell-platform

$ cabal install pandoc

$ pandoc input.md -o output.docx
```

####[proctools](http://www.acloudtree.com/how-to-install-proctools-pkill-pgrep-etc-on-osx-using-homebrew/)

`pkill`や`pgrep`などを使えるようになります。

``` bash
$ brew install proctools

$ pgrep test
```

####[atool](http://www.nongnu.org/atool/)

`atool`は`aunpack`(解凍)や`apack`(圧縮)、`als`(中身の確認)ができるスクリプト群です。

``` bash
$ brew install atool rar

$ aunpack test.rar
```

####[mdfind](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/mdfind.1.html)

`mdfind`は高速でファイル検索を行うコマンドです。

``` bash
$ mdfind . txt
```

####[purge](https://developer.apple.com/library/mac/documentation/darwin/reference/manpages/man8/purge.8.html)

`purge`は、メモリを開放するコマンドです。

``` bash
$ sudo purge
```

####[ctags](http://ctags.sourceforge.net/)

`ctags`は、タグを生成するコマンドです。

``` bash
$ brew install ctags

$ ctags -R
```

####[exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)

`exiftool`は、EXIF情報の確認、削除などを行うコマンドです。

``` bash
$ brew install exiftool

$ exiftool test.png

$ exiftool -overwrite_original -all= ~/Pictures
```

####[imagemagick](http://www.imagemagick.org/)

`imagemagick`は、画像を編集、変換するコマンドです。

``` bash
$ brew install imagemagick

$ mogrify -format png -quality 100 *.jpg
```

####[ffmpeg](http://www.ffmpeg.org/)

`ffmpeg`は、動画を変換するコマンドです。

``` bash
$ brew install ffmpeg

$ for i in *.mp4; do ffmpeg -i $i -vn ${i%.mp4}.mp3; done
```


####[pyful](https://github.com/anmitsu/pyful)

`pyful`は、非常に便利なファイラーです。

``` bash
$ git clone git://github.com/anmitsu/pyful

$ cd pyful

$ sudo python setup.py install -f

$ pyful
```

###<a name="p204">Mavericksの初期設定</a>

####homebrew

Macについては、[Homebrew](http://brew.sh/)を使うことで、アプリをインストールできます。


{% codeblock lang:bash %}
$ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
{% endcodeblock %}

`Xcode`を使っている人は、Xcodeをインストール後に、`Command Line Tools`をインストールします。

{% codeblock lang:bash %}
$ xcode-select --install
{% endcodeblock %}

私の場合、Xcodeは、使いませんので、Command Line Toolsだけをインストールします。

{% codeblock lang:bash %}
$ open -a Safari "https://developer.apple.com/downloads/index.action" && read key

$ hdiutil mount ~/Downloads/*.dmg && killall Finder

$ sudo installer -pkg /Volumes/Command\ Line\ Developer\ Tools/*.pkg -target /Volumes/Macintosh\ HD/
{% endcodeblock %}

認証すら面倒な方は、[airkeepass](https://github.com/syui/airkeepass)などを使って自動化してください。


Homebrewのエラーは、以下のコマンドにて確認できます。エラーが出て、修正の必要性がある場合は、修正してください。

{% codeblock lang:bash %}
$ brew doctor
{% endcodeblock %}

Homebrewは、bundleに対応しています。

{% codeblock lang:bash %}
$ brew bundle ~/dotfiles/bundle/Brewfile
{% endcodeblock %}

以下、インストールファイルの作成です。


{% codeblock lang:bash %}
{% raw %}
$ mkdir -p  ~/dotfiles/bundle

$ cat << EOF > ~/dotfiles/bundle/Brewfile
update
upgrade

tap homebrew/binary || true
tap homebrew/versions || true
tap phinze/homebrew-cask || true

install ack
cask install alfred
cask alfred link

cleanup
EOF
{% endraw %}
{% endcodeblock %}

####setup.sh

更に、こういったbundleファイルは、`install.sh`や`setup.sh`などを作って、自動化しておくと便利です。


[dotfiles](https://github.com/syui/dotfiles)をちょっと作ってあげておきました。


うまく動作しないかもですが、そのうち作りなおすつもりです...。


{% codeblock lang:bash ~/dotfiles/install.sh %}
{% raw %}
#!/bin/sh
if [ `uname` = "Darwin" ]; then

### homebrew
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"

### command line tools
#$ xcode-select --install
open -a Safari "https://developer.apple.com/downloads/index.action" && read key
hdiutil mount ~/Downloads/*.dmg && killall Finder
sudo installer -pkg /Volumes/Command\ Line\ Developer\ Tools/*.pkg -target /Volumes/Macintosh\ HD/

### homebrew cask
cd ~/dotfiles/mac/bundle
brew bundle

### ruby
cd ~/dotfiles/bundle
gem install bundler
bundle install

### python
easy_install pip

### Update
#brew update
#brew upgrade
#brew cleanup

elif [ `uname` = "Linux" ]; then
  sudo pacman -Syy
  sudo pacman -S git vim tmux zsh base-devel lilyterm mozc ibus-mozc yaourt
  #sudo pacman -Syu
  #sudo pacman -Scc
fi

cygcheck -c cygwin > /dev/null 2>&1
if [ $? == 0 ]; then
  apt-cyg install git vim tmux zsh
fi
{% endraw %}
{% endcodeblock %}

{% codeblock lang:bash %}
$ curl -L https://raw.github.com/username/dotfiles/master/setup.sh | sh
{% endcodeblock %}

####wallpaper

私は、共通して、以下の壁紙をなんとなく使っています。一応、オリジナルです。ロゴは、`Arch Linux`のものですが。Archのコミュニティにも一度投稿しています。


{% codeblock lang:bash %}
$ curl -O http://lh5.ggpht.com/-DBe6qOlsFVk/UxE1t1LosJI/AAAAAAAAH1U/lvVKxMKyifA/s0/arch_black.png
{% endcodeblock %}


####system preferences

以下、システム環境設定です。

{% codeblock lang:bash %}
$ open -a "system preferences"
{% endcodeblock %}

> セキュリティとプライバシー -&gt; ファイアウォール

> セキュリティとプライバシー -&gt; プライバシー -&gt; アクセシビリティ

> キーボード -&gt; F1, F2など...

> キーボード -&gt; ショートカット -&gt; すべてのコントロール

> キーボード -&gt; ショートカット -&gt; キーボード -&gt; 一番手前の...


あとは、`TinkerTool`などでカスタマイズします。

{% codeblock lang:bash %}
$ open -a TinkerTool
{% endcodeblock %}

####KeyRemap4MacBook

次に、`KeyRemap4MacBook`の設定です。

設定ファイルを指定の場所`~/Library/Application Support/KeyRemap4MacBook/private.xml`に置きます。

{% codeblock lang:bash %}
$ open -a KeyRemap4MacBook

$ cp ~/dotfiles/mac/Library/Application\ Support/KeyRemap4MacBook/private.xml ~/Library/Application\ Support/KeyRemap4MacBook/
{% endcodeblock %}


ファイルの内容は以下のとおりです。

{% codeblock lang:bash ~/Library/Application\ Support/KeyRemap4MacBook/private.xml %}
{% raw %}
<?xml version="1.0"?>
<root>
    <list>
        <item>
            <name>LeaveInsMode with EISUU(Terminal)</name>
            <identifier>private.app_terminal_esc_with_eisuu</identifier>
            <only>TERMINAL</only>
            <autogen>--KeyToKey-- KeyCode::ESCAPE, KeyCode::ESCAPE, KeyCode::JIS_EISUU</autogen>
            <autogen>--KeyToKey-- KeyCode::J, VK_CONTROL, KeyCode::J, VK_CONTROL, KeyCode::JIS_EISUU</autogen>
        </item>
    </list>
</root>
{% endraw %}
{% endcodeblock %}



これで、`C+j`を押すと、IMEがOFFになります。


その他、このアプリでは、カーソル移動速度(キーリピート)なども変更できます。変更しておきましょう。


####airchrome.zsh

しかし、このブログに貼り付けられているコマンドをコピー、実行するのも面倒な作業です。


したがって、[airchrome.zsh](https://github.com/syui/airchrome.zsh)というものを作ってみました。よろしければ使ってみてください。`zsh`と`Google Chrome`で動作します。


{% codeblock lang:bash %}
$ git clone https://github.com/syui/airchrome.zsh

$ cd airchrome.zsh

$ ./airchrome.setup

$ zsh
{% endcodeblock %}

####airkeepass

初期設定では、Webでの認証が必要になったりすることがあります。


ここで、パスワード入力を自動化する[airkeepass](https://github.com/syui/airkeepass)というツールを作りました。


必要なときにスクリプトから呼び出してやると、初期設定が楽になるかもしれません。


{% codeblock lang:bash %}
$ git clone https://github.com/syui/airkeepass

$ cd airkeepass

$ ./airkeepass
{% endcodeblock %}


###<a name="p205">Mavericksにインストールしたアプリ</a>

{% codeblock lang:bash ~/dotfiles/mac/bundle/Brewfile %}
#sort ~/dotfiles/mac/bundle/Brewfile -uo ~/dotfiles/mac/bundle/Brewfile

update
upgrade

tap homebrew/binary || true
tap homebrew/versions || true
tap phinze/homebrew-cask || true

install ack
install apple-gcc42
install aspell
install atool
install autoconf
install binutils
install cmigemo
install comix
install coreutils
install ctags
install curl
install ffmpeg
install figlet
install fontforge
install gibo
install gist
install git
install global
install gnu-sed
install gnupg
install graphicsmagick
install heroku-toolbelt
install hub
install imagemagick
install jq
install jsl
install kindlegen
install lv
install markdown
install mcrypt
install mercurial
install mplayer
install nginx
install node
install openssl
install phpenv
install pkg-config
install plenv
install postgresql
install qt
install rbenv
install readline
install reattach-to-user-namespace
install sbt
install scala
install stunnel
install tig
install tmux
install tree
install unrar
install vim
install w3m
install webkit2png
install wget
install xz
install zsh
install gauche
install brew-cask
install swftools
install youtube-dl

cask install adium
cask install adobe-reader
cask install alfred
cask install appcleaner
cask install bettertouchtool
cask install ccleaner
cask install cheatsheet
cask install clamxav
cask install clipmenu
cask install dropbox
cask install firefox
cask install flash
cask install flip4mac
cask install gimp
cask install github
cask install google-chrome
cask install google-drive
cask install google-japanese-ime
cask install grandperspective
cask install growlnotify
cask install handbrake
cask install hipchat
cask install intellij-idea-community
cask install iterm2
cask install keepassx
cask install keyremap4macbook
cask install kobito
cask install libreoffice
cask install limechat
cask install lyn
cask install macvim
cask install mplayerx
cask install nosleep
cask install openoffice
cask install opera
cask install quicksilver
cask install ripit
cask install sequel-pro
cask install shiftit
cask install silverlight
cask install simple-comic
cask install skitch
cask install skype
cask install sourcetree
cask install sublime-text
cask install sublime-text3
cask install the unarchiver
cask install tinkertool
cask install trailer
cask install vagrant
cask install virtualbox
cask install vlc
cask install xtrafinder

#cask alfred link
#cleanup
{% endcodeblock %}


ちなみに、行頭のコマンドは重複を削除するものです。


この点、必須コマンドとインストールアプリの記述を分けておくと便利かもです。


具体的には、以下の様な感じです。

{% codeblock lang:bash ~/dotfiles/mac/bundle/Gemfile.sh %}
update
upgrade
tap homebrew/binary || true
tap homebrew/versions || true
tap phinze/homebrew-cask || true
{% endcodeblock %}

{% codeblock lang:bash ~/dotfiles/mac/bundle/Gemfile.app %}
install gauche
cask install xtrafinder
{% endcodeblock %}

{% codeblock lang:bash ~/dotfiles/mac/bundle/Gemfile.sh %}
{% raw %}
#!/bin/bash
bpath="~/dotfiles/mac/bundle"

sort $bpath/Brewfile.app -uo $bpath/Brewfile.app
rm $bpath/Brewfile > /dev/null 2>&1
cat $bpath/Brewfile.back > $bpath/Brewfile
cat $bpath/Brewfile.app >> $bpath/Brewfile
cd $bpath
brew bundle
{% endraw %}
{% endcodeblock %}

これで、アプリの重複記述を心配する必要はなくなります。


###<a name="p206">MavericksをVirtualBoxにインストールする</a>

Mavericksは、仮想環境に2つまでインストールできます。あくまで、Mac機にのみですが。


現在確認している VirtualBox での Mavericks インストーラー起動のための要件は以下のとおりです。

> ・MacBook 2013 以外でVirtualBoxを使うこと

> ・Operating System Version: Mac OS X (64 bit)

> ・Base Memory: 2048 MB (larger is better)

> ・EFI 有効化

> ・場合によってチップセット ICH9 から PIIX3 に変更


ほとんどがデフォルトの設定そのままいけるのですが、`MacBook 2013 以外`という要件にハマりました。


{% codeblock lang:bash %}
$ system_profiler SPMemoryDataType

$ virtualbox --help | grep "Oracle VM VirtualBox Manager"

$ rvm install 1.9.2

$ rvm use 1.9.2

$ gem install iesd

$ iesd -i /Applications/Install\ OS\ X\ Mavericks.app -o Mavericks.dmg -t BaseSystem
{% endcodeblock %}


まず、`SPMemoryDataType`を調べています。

ECCメモリを持っているかいないかで実行するコマンドが変化してきます。

``` bash
# ECCメモリを持っていない
$ iesd -i /Applications/Install\ OS\ X\ Mavericks.app -o Mavericks.dmg -t BaseSystem

# ECCメモリを持っている
$ iesd -i /Applications/Install\ OS\ X\ Mavericks.app -o Mavericks.dmg -t BaseSystem –remove-kexts AppleTyMCEDriver.kext
```

私の場合、 MacBookAir Mid 2012 では VirtualBox で Mavericks のインストーラーを起動することに成功しましたが、 MacBookAir Mid 2013 では上手くいきませんでした。


これは、イメージ実行の問題なので、イメージ作成は2012, 2013どちらで行っても構いません。


さらに、上手くインストール画面が表示されても、新たな問題が発生しました。


具体的には、ディスクユーティリティを使ってディスクを消去できない問題です。


これは、一旦、 Mavericks のインストーラーを再起動することで解決しました。


ちなみに、上記は、 VirtualBox からの再起動ではなく、あくまで Mavericks インストーラーの再起動です。


<a href="http://www.robertsetiadi.net/install-os-x-virtualbox/" target="_blank">How to install OS X on VirtualBox - Robert Setiadi Website</a>


##Windows | Windows7

|Windows7|
|---|
|[Windowsで使っているアプリ](#p300)
|[VirtualBox Guest Additions](#p301)
|[Update](#p302)
|[Setting](#p303)
|[Sysinternals Suite](#p304)
|[Microsoft Security Essentials](#p305)
|[PowerShell](#p306)
|[Chocolatey](#p307)
|[Cygwin](#p308)
|[Console Z](#p309)
|[OpenSSH](#p310)
|[AutoHotkey](#p312)
|[スタートアップ](#p311)


###<a name="p300">Windowsで使っているアプリ</a>

####[Console 2](http://sourceforge.net/projects/console/)

Windowsで使えるターミナルアプリ。ウィンドウを透過したり、キーマップを設定したりと基本的なことができます。

####[Cygwin](http://www.cygwin.com/)

Linux環境をWindows上で再現するためのアプリ。快適です。

####[Microsoft Security Essentials](http://windows.microsoft.com/ja-jp/windows/security-essentials-download)

Windowsで使える公式セキュリティ対策ソフト。

####[PowerShell 4.0](http://www.microsoft.com/ja-jp/download/details.aspx?id=40855)

Windowsで唯一まともに動くシェル。多分、一番使用するであろうアプリ。

####[Chocolatey](https://chocolatey.org/)

Windowsのパッケージ管理アプリ。GUIアプリも自動でインストールしてくれます。

####[Sysinternals Suite](http://technet.microsoft.com/ja-jp/sysinternals/bb842062.aspx)

Windowsで使えるミリソフト群。とてつもなく有効なアプリばかり。

####[AutoHotkey](http://www.autohotkey.com/)

Windowsのキー操作を自動化するためのアプリです。スクリプトを書くことで自動化を実現できます。

####[Greenshot](http://getgreenshot.org/)

Windowsでスクリーンショットを撮影するためのアプリです。

####[Gow](https://github.com/bmatzelle/gow)

> Windowsのコマンドプロンプト上で基本的なLinuxコマンドを実現するためのアプリです。

####[MinGW](http://www.mingw.org/)

> GNUの開発環境を使ってWindowsの開発を支援するためのツール群です。

####[Google Chrome](http://www.google.co.jp/intl/ja/chrome/browser/)

> 定番のブラウザです。ブラウザのWebコンソールが一番使いやすいので、このアプリ一択です。ブログとかやっている人は、分かる人多いかもですね。

####[Firefox](http://www.mozilla.jp/firefox/)

どちらかと言うと、Chromeよりも、Chromium。ChromiumよりもFirefoxのほうが好きですね。個人的には。

####[PictBear](http://www.forest.impress.co.jp/library/software/pictbear/)

軽量かつ安定の画像編集アプリ。個人的には一番良く使う手軽なソフトです。

####[AzPainter](http://www.forest.impress.co.jp/library/software/azpainter/)

2番目に使う画像編集アプリ。堅実で細かい部分で割と気が聞いています。

####[Paint.NET](http://www.forest.impress.co.jp/library/software/paintdotnet/)

> 定番の画像編集アプリ。個人的にはあまり合わないので、あまり使えない。

####[Lhaplus](http://www.forest.impress.co.jp/library/software/lhaplus/)

個人的にはお勧めの圧縮、解凍ソフトです。ただし、バージョンによっては、脆弱であったりしますので、解凍するファイルには、気をつけてください。

####[WinRAR](http://www.forest.impress.co.jp/library/software/winrar/)

> RAR形式の圧縮に対応する圧縮、解凍ソフトです。こちらのソフトも扱いには注意が必要です。なぜなら、多くのコンピュータウィルスは、圧縮ファイルに偽装されている確率が非常に高いからです。特に、WinRARは狙われやすいソフトでもあります。

####[CCleaner](https://www.piriform.com/ccleaner)

定番のお掃除ソフト。一時ファイル、Cookieなどを削除してくれます。レジスタの編集を補助してくれたり、スタートアップを表示してくれたりと色々と便利です。

####[Glary Utilities](http://www.forest.impress.co.jp/library/software/glaryutils/)

> 昔愛用していたクリーナーソフト。非常におすすめでした。

####[KeySwap](http://www.vector.co.jp/soft/winnt/util/se228667.html)

MacBookAirを使用しているので、どうしてもキーの変更が必要になってくる場面があります。そんな時は、このソフトを使って、変更しています。

####[MetaTrader4](http://www.metatrader4.com/)

非常に高機能なチャートソフト。Wineでも動作するし、最近ではiOS, Androidにも対応した。ちなみに、ショートカットキーの確認は、F1を押して、ヘルプを表示し、「Client Terminal  / ユーザインターフェイス / ファーストナビゲーション」より。


###<a name="p301">VirtualBox Guest Additions</a>

####Driverのインストール

`Windows7`は、仮想環境上で起動します。


まずは、これを実行しなければ始まりません。VirtualBoxで動作させるOSには必ずと言っていいほど実行しましょう。


実行方法としては、`Host+D`です。


その後、コンピューターを`Win+E`で開きます。そこにデバイスが表示されているはずです。これを実行します。各種ドライバがインストールされます。




####Window Aeroの有効化

なお、ウィンドウの透過度を設定する`Aero`を有効にしたい場合は、VirtualBoxのWindowsイメージの設定でディスプレイのビデオにある3Dの設定を有効にし、3Dのドライバをインストールしましょう。





####ファイル共有

ファイル共有及び、共有フォルダの作成は、VirtualBoxのメニューを開けばわかると思います。ただし、共有フォルダを扱いやすくするためには、右クリック &gt; ネットワークドライブ割り当てを行ってください。デフォルト設定でもどこかに割り当てられてるものですが。




####シームレスモード

VirtualBoxにはシームレスモードといって、アプリウィンドウをホストOSに表示することができます。


これを使用することで、まるでWindows上で、Linuxのアプリを動かしているように操作することができます。


通常は、`Host`+`L`を押せば、有効にできると思います。

###<a name="p302">Update</a>

まず行うべきなのが、Update(アップデート)です。`Win+Shift+4`を押し、コントロールパネルを開きます。ここで、小さいアイコンを選択します。そして、`Windows Update`を選択します。





しかし、アップデートにはかなりの時間がかかります。


以下、その間に行うおすすめの設定を紹介しておきます。


###<a name="p303">Setting</a>


マシンのスペックが弱い場合は、パフォーマンスなどを変更します。


具体的には、コントロールパネルを開き、そこで以下の項目を選択して適当に設定します。


> パフォーマンスの情報とツール -&gt; 視覚効果の調整 -&gt; パフォーマンスを優先する

> フォルダオプション -&gt; 表示 -&gt; 保護、拡張子、常にメニュー、隠しファイル


フォントが汚くなりますが、後述する`MacType`で割りと良くなります。


※ MacTypeがコンピュータウィルスとして検出されました。直ちに、利用を停止することをおすすめします。


フォントを変更したい方は、以下の記事を参考にしてみてください。


<a href="http://kirmav.blogspot.jp/2010/10/windows-7-64bit.html" target="_blank">萌えないごみの日: Windows 7 (64bit) でシステムフォントの全入れ替え！</a>


###<a name="p304">Sysinternals Suite</a>


Windowsの場合、これだけではカスタマイズを行ったとは言えません。Windowsをさらに最適化させるには、[Sysinternals Suite](http://technet.microsoft.com/ja-jp/sysinternals/bb842062.aspx)というツールが必要になります。


このツール(正確にはツール群)は、ダウンロードする必要がありますが、これがないと、私はWindowsを使いこなすことが全くできません...。


ちなみに、Windowsでは、実行ファイルを`C:\Program Files`に置くのが慣習です。


ここで、おすすめのアプリは、以下のとおりです。

アプリ|内容
|---|---|
AccessEnum|システムのディレクトリ、ファイル、およびレジストリ キーに対してどのユーザーがどのようなアクセス権を持っているかを確認できる
Autoruns|システムの起動時やユーザーのログイン時に自動的に起動するように構成されているプログラムを確認する
Process Explorer|プロセスが開いたファイル、レジストリ キーなどのオブジェクト、読み込んだ DLL などを調べる
Process Monitor|ファイル システム、レジストリ、プロセス、スレッド、および DLL の活動をリアルタイムで監視する
RAMMap|高度な物理メモリ利用状況分析ユーティリティ
WinObj|究極のオブジェクト マネージャーの名前空間ビューアー
Desktops|最大で 4 つの仮想デスクトップを作成


その他にも使えるツールばかりですが、一番お勧めなおは、`Process Explorer`ですかね。


###<a name="p305">Microsoft Security Essentials</a>


次にインストールするべきなのが[Microsoft Security Essentials - Microsoft Windows](http://windows.microsoft.com/ja-jp/windows/security-essentials-download)です。





###<a name="p306">PowerShell</a>

[PowerShell 4.0](http://www.microsoft.com/ja-jp/download/details.aspx?id=40855)が出ていますので、インストールしてみることにしましょう。多分、Windowsでは一番に常用することになるアプリです。



ただ、ターミナルが終わっているので、変更しましょう。おすすめするのは、`Cosole Z`または、`Mintty`です。下記で紹介。


###<a name="p307">Chocolatey</a>

まずは、[Chocolatey](https://chocolatey.org/)のインストールからですね。これは、アプリをコマンド一つでダウロードするPackageManager(パッケージマネージャー)のようなものです。


`Wind+R`を押して、`cmd`を起動し、以下のコマンドを実行します。

{% codeblock lang:bash %}
{% raw %}
> @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin

> cinst ccleaner dropbox python git vlc GoogleChrome 7zip curl gimp greenshot ConsoleZ cygwin
{% endraw %}
{% endcodeblock %}


###<a name="p308">Cygwin</a>

次に、[Cygwin](http://cygwin.com/packages/)を立ち上げて、以下を実行します。これは、Windows上でLinux環境を再現するものです。


`Win+R` | `C:\Cygwin\Cygwin.bat`


しかし、デフォルトターミナルがあまりに貧弱なので、まずは`minnty`を起動しています。


{% codeblock lang:bash %}
$ mintty
{% endcodeblock %}


##<a name="p308">apt-cyg</a>

次に、パッケージを簡単にインストールできるようにしておきましょう。

{% codeblock lang:bash %}
$ cygstart /cygdrive/c/Cygwin/cygwinsetup -q -P wget, curl

$ wget http://apt-cyg.googlecode.com/svn/trunk/apt-cyg

$ chomd +x apt-cyg

$ mv apt-cyg /usr/bin
{% endcodeblock %}


これで、`apt-cyg`コマンドを使えるようになりました。

ちなみに、`wget`のインストールは、本来なら下記のようなコマンド(powershell)になります。

{% codeblock lang:bash %}
{% raw %}
C:\Cygwin\cygwinsetup.exe -q -P wget
{% endraw %}
{% endcodeblock %}


次に、必要なツールをインストールしていきましょう。

{% codeblock lang:bash %}
$ apt-cyg install zsh vim tmux git
{% endcodeblock %}


###<a name="p309">Console Z</a>

`Console Z`とは、`Console 2`を元に作ったターミナルです。バックグラウンドでcmdまたは、powershellを動かしてるみたいですね。





なお、ターミナルでは、`Mintty`もお勧めです。


ConsoleZの設定としては、以下のとおりです。


####Shellの設定

Cygwinの`zsh`を使いたい場合は、以下の様なパスを指定します。


{% codeblock lang:bash %}
C:\Cygwin\bin\zsh.exe --login -i
{% endcodeblock %}




####複数タブの起動

ConsoleZのショートカットを作成し、パスを以下のような感じにします。すると、タブを複数指定して起動できます。ちなみに、ショートカットを作成するのは実行ファイルを右クリックです。


{% codeblock lang:bash %}
C:\Chocolatey\lib\ConsoleZ.1.10.0.14089\tools\Console.exe -t "cygwin" -t "powershell"
{% endcodeblock %}


<a href="http://tech.guitarrapc.com/entry/2014/01/29/061245" target="_blank">PowerShell でショートカットを作成する - tech.guitarrapc.cóm</a>


####日本語文字のズレを解消

2バイト文字がずれる問題の対処法です。マニュアルに書いてあるとおりにします。

> 右クリック -&gt; View -&gt; Console Window

> cmdが起動されるので、`Alt+Space`、`p(プロパティ)`の順にキーを押します。

> `Tab+Ctrl`を押して、表示 -&gt; フォントを「MS ゴシック」などの日本語フォントに変更します。


あとは、Console Zのフォントを設定してください。



ちなみに、フォントを増やすには、以下のとおりにします。

> `Win+R` | `regedit`

> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Console\TrueTypeFont`

> 新規 -> 文字列 -> '932.1'='IPAゴシック'

> Windowsを再起動


<a href="http://sandbox.hatenadiary.com/entry/2013/06/01/165431" target="_blank">Windows8：コマンドプロンプトのフォント変更 - すなばあそび。</a>


####アイコンを設定する

また､iconを設定できます｡ [IconsExtract](http://www.nirsoft.net/utils/iconsext.html)を使うと実行ファイルから簡単に取得できます｡

{% codeblock lang:bash %}
$ wget http://www.nirsoft.net/utils/iconsext.zip

$ unzip iconsext.zip

$ chmod +x iconsext.exe

$ cygstart iconsext.exe
{% endcodeblock %}



###<a name="p310">OpenSSH</a>

####接続不能編

CygwinのOpenSSHを利用し、SSH Serverを立ち上げてみます。

前提として、VirtualBoxの設定を行います。[こちら](#network)を参考にしてください。


{% codeblock lang:bash サーバー %}
$ apt-cyg install openssh

$ ssh-host-config -y

$ cygrunsrv -S sshd
{% endcodeblock %}

ファイアウォールの設定を変更します。ポート`22`を開けましょう。

{% codeblock lang:bash クライアント %}
$ ssh -v cyg_server@192.168.56.101
{% endcodeblock %}


しかし、何故かアクセス出来ないという...。接続が完了しても、すぐに閉じてしまう。原因は多分、localeの設定です。


結局、設定ファイルを変更したり、いろいろ試してみたのですが、無理でした。

{% codeblock lang:bash C:\Cygwin/Cygwin.bat %}
@echo off

C:
chdir C:\cygwin\bin
set CYGWIN=binmode ntsec tty
bash --login -i
{% endcodeblock %}


{% codeblock lang:bash /etc/sshd_config %}
StrictModes no

RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

PasswordAuthentication yes
Port 22
{% endcodeblock %}


####接続可能編

単にパスワードが設定されてなかっただけの問題だったみたいです。よくわからない...。一応、どちらも管理者として実行をやってみました。これがほんとうに必要なのか分かりませんが。

{% codeblock lang:bash サーバー %}
$ passwd
{% endcodeblock %}

そもそも設定された名前(cyg_server)がホスト名になるわけじゃなかったみたいです。どうやら、Windowsのユーザー名(syui)を使うみたいですね。

{% codeblock lang:bash クライアント %}
$ ssh -v syui@192.168.56.101
{% endcodeblock %}


<a href="http://docs.oracle.com/cd/E18930_01/html/821-2426/gksiy.html" target="_blank">Setting Up Cygwin SSH on Windows - Oracle GlassFish Server 3.1-3.1.1 High Availability Administration Guide</a>


####セキュリティ編

パスワードでの接続が可能となったので、セキュリティを変更していきます。


まず、公開鍵の発行と送信です。

{% codeblock lang:bash クライアント %}
$ ssh-keygen -t rsa

$ brew install ssh-copy-id

$ ssh-copy-id -i ~/.ssh/id_rsa.pub syui@192.168.56.101
{% endcodeblock %}


次に、サーバーを停止し、設定ファイルを編集します。

{% codeblock lang:bash サーバー %}
$ cygrunsrv -E sshd

$ vim /etc/sshd_config
{% endcodeblock %}

{% codeblock lang:bash /etc/sshd_config %}
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

PasswordAuthentication no
Port 55101
{% endcodeblock %}

ファイアウォールでポート`55101`を開けます。


あとは、サーバーを起動し、クライアントから接続するだけです。

{% codeblock lang:bash サーバー %}
$ cygrunsrv -S sshd
{% endcodeblock %}

{% codeblock lang:bash クライアント %}
$ ssh syui@192.168.56.101 -p 55101
{% endcodeblock %}


####Windowsの自動ログイン

ちなみに、パスワードが設定されると、自動でログインできなくなります。Windowsの自動ログインを解除するには、以下の手順が必要です。

> 1. [スタート] ボタンをクリックし、「netplwiz」と入力して、Enter キーを押します。

> 2. [ユーザー アカウント] ダイアログ ボックスで、自動的にログオンするときに使うアカウントをクリックします。設定を変更できる場合は、[ユーザーがこのコンピューターを使うには、ユーザー名とパスワードの入力が必要] チェック ボックスをオフにします。

> 3. [OK] をクリックします。

> 4. [自動ログオン] ダイアログ ボックスでユーザーのパスワードを 2 回入力し、[OK] をクリックします。


<a href="http://technet.microsoft.com/ja-jp/magazine/ee872306.aspx" target="_blank">Windows 7 で自動的にログオンするようにユーザー アカウントを構成する</a>


####PowerShellServer

[PowerShellServer](http://www.powershellserver.com/)というものがあるらしいです。



###<a name="p312">AutoHotkey</a>

このソフトは、キー入力を自動化するために使われるソフトです。常駐型で、ソフトごとにキーなどを入れ替えたりできます。

まずは、[チュートリアル](http://www.autohotkey.com/docs/Tutorial.htm)を読むのが早いです。

通常は、常駐アイコンから、`右クリック -> Edit This Script`でスクリプトを書きます。リロードも右クリックからできます。


書き方は以下のとおり。

```
+l::Send {F12} ;Shift+lでF12を押す
+h::+F12 ;Shift+hでShift+F12を押す
+k::left ;Shift+kで←を押す
+j::right ;Shift+jで→を押す
+f::Send,!fi{Enter} ;Shift+fでAlt+f, i, Enterの順に押す
```

|キー|表現|
|---|---|
|Ctrl|^
|Shift|+
|Alt|!
|Win|#


###<a name="p311">スタートアップ</a>

Windowsで起動時に実行するアプリは、`スタートアップ`フォルダに入れます。私が起動時に実行するアプリとしては、以下の様な感じです。


> Desktops, Cosole Z, Dropbox


スタートアップフォルダは、`C:\Users\syui\AppData\Roaming\Microsoft\Windows\Start Menu\Programs`にあります。


また、必要ないスタートアップは、`CCleaner`などを使って消しておきましょう。


##Linux | Manjaro Linux

|Manjaro Linux|
|---|
|[Arch Linuxで使っているアプリ](#p4xx)
|[Manjaro LinuxをMacBookAirに直接インストールする方法](#p400)
|[Manjaro Linux Awesomeの基本操作](#p401)
|[Manjaro LinuxをMacの仮想環境上で動作させる方法](#p413)
|[pacman](#p402)
|[ibus](#p403)
|[locale](#p404)
|[xmodmap](#p405)
|[awesome](#p406)
|[spacefm](#p407)
|[firefox](#p408)
|[lilyterm](#p409)
|[zsh](#p410)
|[vim](#p411)
|[tmux](#p412)

###<a name="p4xx">Arch Linuxで使っているアプリ</a>

Manjaro Linuxといっても、認知度はほとんどありませんので、表題をArch Linuxとしています。

####[Awesome](https://wiki.archlinux.org/index.php/Awesome_(%E6%97%A5%E6%9C%AC%E8%AA%9E)

Linuxで動作するウィンドウマネージャー。いわゆるタイル型と言われて、ウィンドウを定形、キー操作できるのが特徴。

``` bash
$ sudo pacman -S awesome
```

####[SLiM](https://wiki.archlinux.org/index.php/SLiM_(%E6%97%A5%E6%9C%AC%E8%AA%9E)

Linuxで動作するログインマネージャー。カッコイイ!!

``` bash
$ sudo pacman -S slim
```

####[SpaceFM](http://ignorantguru.github.io/spacefm/)

Linuxで動作するファイルマネージャ。軽量で処理が早く、多くの操作に適している。

``` bash
$ sudo pacman -S spacefm
```

####[lilyterm](https://wiki.archlinux.org/index.php/LilyTerm)

Linuxで動作するターミナルアプリ。これ以外考えられない。

``` bash
$ sudo pacman -S lilyterm
```

####[dwb](http://portix.bitbucket.org/dwb/)

Linuxで動作する軽量のインターネットブラウザ。viのキーバインドが使える。[こちら](http://qiita.com/syui/items/02b2064afb4dc8393226)の記事にまとめたので、使い方がわからない人は、読んでほしい。

``` bash
$ sudo pacman -S dwb
```

####[canto](http://codezen.org/canto/)

スタイリッシュなRSSリーダー。とても現代風。

``` bash
$ sudo yaourt -S canto
```

####[jdownloader](https://wiki.archlinux.org/index.php/JDownloader)

Javaで動作するダウンロードマネージャーです。ファイルのダウンロードはこれ一本に任せましょう。

``` bash
$ sudo pacman -S jre7-openjdk

$ sudo yaourt -S jdownloader
```

###<a name="p400">Manjaro LinuxをMacBookAirに直接インストールする方法</a>




####Manjaro Linuxのインストール

<a href="http://sourceforge.net/projects/manjaro-awesome-respin/files/" target="_blank">Manjaro Awesome WM Respin</a>

<a href="https://github.com/Culinax/manjaro-awesome-respin" target="_blank">Culinax/manjaro-awesome-respin · GitHub</a>


まず、インストールUSBを作成しなければなりません。イメージをダウンロードして、USBに書き込みましょう。


{% codeblock lang:bash %}
$ hdiutil convert -format UDRW -o manjaro-awesome-0.8.8-b4.1-x86_64.dmg manjaro-awesome-0.8.8-b4.1-x86_64.iso

$ diskutil list

$ sudo diskutil umountDisk /dev/disk1

$ sudo dd if=./manjaro-awesome-0.8.8-b4.1-x86_64.dmg of=/dev/disk1 bs=1m
{% endcodeblock %}

次に、MacBookAirに作成したUSBを挿しこみます。`Alt`を押しっぱなしにして、電源を入れ、`Manjaro Linux`を起動します。


そして、インストーラーを起動します。




インストールで重要なのは、①EFIサポートを選択すること。



ディスクパーティションでは、②オートを選択すること。





ブートローダーのインストールは、直にインストールする場合は、③UEFIを選択すること。






以上です。後の各項目はなんとかなるでしょう。設定しなくても良い項目も多いのですが、必要ある場合は、各自設定しましょう。また、ユーザー設定以外、あとで変更することは可能です。


<a href="http://mba-hack.blogspot.jp/2014/01/manjaro-linux-vol3.html" target="_blank">Manjaro Linuxのカスタマイズ vol.3</a>


###<a name="p401">Manjaro Linux Awesomeの基本操作</a>

まずは、基本操作を確認しておきましょう。これは、`awesome`というWindow Manager(ウィンドウマネージャー)の操作方法です。


デフォルトでは、`Mod4 -> Command`です。

キー|効果
|---|---|
Esc|キャンセル
Mod4+Enter|Terminal (ターミナル)
Mod4+d|Browser (ブラウザ)
Mod4+p|DMenu (D-メニュー)
Mod4+w|Open Menu (メニュー)
Mod4+t|File Manager (ファイルマネージャ)
Mod4+j|Focus Next (次のウィンドウへ)
Mod4+k|Focus Prev (前のウィンドウへ)
Mod4+→|Desktop Next (次のデスクトップへ)
Mod4+h|Decrease Master (ウィンドウを拡張)
Mod4+i|Increase Master (ウィンドウを縮小)
Mod4+f|Set client fullscreen (現在のウィンドウをフルスクリーンに)
Mod4+Space|Cycle Lagouts (ウィンドウの並び替え)
Mod4+Ctrl+r|Restart Awesome (再起動)
Mod4+Shift+q|Logout (ログアウト、sでシャットダウン、rで再起動)

その他の基本操作は以下のとおりになっています。これらは、個別のアプリによって設定されています。よって、アプリによっては、効果が異なる場合があります。しかし、多くのアプリには、共通するキーが多いのも事実です。


キー|効果
|---|---|
Enter|選択、実行
Space|プレビュー
Ctrl+c|クリップボードにコピー
Ctrl+v|クリップボードから呼び出し
Ctrl+z|戻る
F1|明るさを下げる
F2|明るさを上げる
F10|音量を下げる
F11|音量を上げる
F12|音量を最大に


###<a name="p402">pacman</a>


最初に、自動実行されるスクリプトがあります。これは、ダウンロードするツールやMacBook用のドライバを自動でインストール、設定してくれるものです。


しかし、このスクリプトを有効に使うには、まずは、パッケージ管理システムを設定していかなければなりません。


よって、まず、パッケージ管理システムの設定です。

{% codeblock lang:bash %}
$ sudo vi /etc/pacman.conf
{% endcodeblock %}


まず、一番下辺りの行をコメントアウトしたり、`mozc`インストール用の設定を書き足します。


{% codeblock lang:html /etc/pacman.conf %}
#
# /etc/pacman.conf
#
# See the pacman.conf(5) manpage for option and repository directives

#
# GENERAL OPTIONS
#
[options]
# The following paths are commented out with their default values listed.
# If you wish to use different paths, uncomment and update the paths.
#RootDir     = /
#DBPath      = /var/lib/pacman/
#CacheDir    = /var/cache/pacman/pkg/
#LogFile     = /var/log/pacman.log
#GPGDir      = /etc/pacman.d/gnupg/
HoldPkg     = pacman glibc manjaro-system
# If upgrades are available for these packages they will be asked for first
SyncFirst   = archlinux-keyring manjaro-keyring manjaro-system pacman
#XferCommand = /usr/bin/curl -C - -f %u > %o
#XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
#CleanMethod = KeepInstalled
#UseDelta    = 0.7
Architecture = auto

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
#IgnorePkg   =
#IgnoreGroup =

#NoUpgrade   =
#NoExtract   =

# Misc options
#UseSyslog
#Color
#TotalDownload
CheckSpace
#VerbosePkgLists

# By default, pacman accepts packages signed by keys that its local keyring
# trusts (see pacman-key and its man page), as well as unsigned packages.
SigLevel    = Required DatabaseOptional
LocalFileSigLevel = Optional
#RemoteFileSigLevel = Required

# NOTE: You must run `pacman-key --init` before first using pacman; the local
# keyring can then be populated with the keys of all official Manjaro Linux
# packagers with `pacman-key --populate archlinux manjaro`.

#
# REPOSITORIES
#   - can be defined here or included from another file
#   - pacman will search repositories in the order defined here
#   - local/custom mirrors can be added here or in separate files
#   - repositories listed first will take precedence when packages
#     have identical names, regardless of version number
#   - URLs will have $repo replaced by the name of the current repo
#   - URLs will have $arch replaced by the name of the architecture
#
# Repository entries are of the format:
#       [repo-name]
#       Server = ServerName
#       Include = IncludePath
#
# The header [repo-name] is crucial - it must be present and
# uncommented to enable the repo.
#

[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[extra]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[community]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs

#[infinality-bundle]
#SigLevel = Never
#Server = http://ibn.net63.net/infinality-bundle/x86_64

#[infinality-bundle-multilib]
#SigLevel = Never
#Server = http://ibn.net63.net/infinality-bundle-multilib/x86_64

#[infinality-bundle-fonts]
#SigLevel = Never
#Server = http://ibn.net63.net/infinality-bundle-fonts

[pnsft-pur]
SigLevel = Optional TrustAll
Server = http://downloads.sourceforge.net/project/pnsft-aur/pur/$arch
{% endcodeblock %}

次に、`pacman`のミラーサーバーの設定です。

{% codeblock lang:bash %}
$ sudo vi /etc/pacman-mirrors.conf
{% endcodeblock %}


{% codeblock lang:bash /etc/pacman-mirrors.conf %}
##
## /etc/pacman-mirrors.conf
##

## Branch Pacman should use (stable, testing, unstable)
Branch=stable

## Generation method
## 1) rank   - rank mirrors depending on their access time
## 2) random - randomly generate the output mirrorlist
Method=rank

## Specify to use only mirrors from a specific country
## Disabled by default
OnlyCountry=Japan

## Input mirrorlist directory
MirrorlistsDir="/etc/pacman.d/mirrors"

## Output mirrorlist
OutputMirrorlist="/etc/pacman.d/mirrors/Japan"
{% endcodeblock %}

これが完了すると、起動時に自動実行される設定スクリプトを有効に使えるようになります。


各自、インストールしたいものを選択したり、MacBook用のドライバなどをインストールしてきましょう。


次に、インストール漏れのツールをインストールしてきます。

{% codeblock lang:bash %}
$ sudo pacman -Syy

$ sudo pacman -S lilyterm yaourt mozc ibus-mozc firefox jq

$ sudo pacman -Syu

$ sudo pacman -Scc
{% endcodeblock %}


###<a name="p403">ibus</a>

次に、日本語入力の設定です。具体的には、`ibus-mozc`を使います。デーモンで起動するようにしました。


{% codeblock lang:bash %}
$ ibus-setup
{% endcodeblock %}







なお、ここでは、2つのショートカットキーを設定してください。何故か一つだけでは、切り替えられません。


あとは、Xのデーモンで起動するようにします。

{% codeblock lang:bash %}
$ sudo touch  /etc/X11/xinit/xinitrc.d/99-ibus

$ sudo chmod +x !$

$ sudo vim !$
{% endcodeblock %}


{% codeblock lang:bash /etc/X11/xinit/xinitrc.d/99-ibus %}
#!/bin/bash
export XMODIFIERS="@im=ibus"
export GTK_IM_MODULE="ibus"
export QT_IM_MODULE="xim"
ibus-daemon -d -x
{% endcodeblock %}

そして、以下のファイルの最後の行を書き換えます。

{% codeblock lang:bash ~/.xinitrc %}
- exec "$1"
+ exec "awesome"
{% endcodeblock %}

Xデーモンで起動する場合は、設定ファイルには、書かなくても良いですのが、一応。

{% codeblock lang:bash ~/.bashrc %}
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
{% endcodeblock %}

###<a name="p404">locale</a>

日本語のための設定は以下のように特定のファイルを書き換えたり、コメントアウトします。

{% codeblock lang:bash /etc/locale.gen %}
ja_JP.EUC-JP EUC-JP
ja_JP.UTF-8 UTF-8
{% endcodeblock %}

{% codeblock lang:bash /etc/locale.conf %}
LANG=ja_JP.UTF-8
LC_MESSAGES=en_US.UTF-8
{% endcodeblock %}

設定を読み込みます。

{% codeblock lang:bash %}
$ sudo locale-gen
{% endcodeblock %}

###<a name="p405">xmodmap</a>

次に、キーマップの設定です。

{% codeblock lang:bash %}
$ cd

$ cp /usr/share/kbd/keymaps/i386/qwerty/jp106.map.gz .

$ gunzip jp106.map.gz

$ mv jp106.map jp106_mac.map

$ vim jp106_mac.map
##########################################
# keycode  58 = Caps_Lock 行を編集
keycode  58 = Control
# keycode  89 = backslash underscore 行を編集
keycode  89 = underscore
##########################################

$ gzip jp106_mac.map

$ sudo mv jp106_mac.map.gz /usr/share/kbd/keymaps/i386/qwerty

$ sudo vim /etc/vconsole.conf
##########################################
KEYMAP="jp106_mac"
##########################################

$ sudo vim /etc/X11/xorg.conf.d/20-keyboard.conf
##########################################
Section "InputClass"
Identifier "system-keyboard"
MatchIsKeyboard "on"
Option "XkbModel" "jp106_mac"
Option "XkbLayout" "jp"
#Option "XkbVariant" ""
EndSection
##########################################

$ xmodmap -pke > ~/.xmodmap2

$ vim ~/.xmodmap1
##########################################
keycode 232 = F1 NoSymbol F1
keycode 233 = F2 NoSymbol F2
keycode 128 = F3 NoSymbol F3
keycode 212 = F4 NoSymbol F4
keycode 66 = Control_L NoSymbol Control_L
keycode 62 = Delete NoSymbol Delete
clear Lock
add Control = Control_L
##########################################
{% endcodeblock %}

`xmodmap1`には、F1-F4までのキーを書いています。デフォルトでは、Macに対応していますので、音量や明るさなどを調整します。しかし、たまに、F1-F4を使用したいことがあるので、設定します。


これらを切り替える方法としては、私は、ウィンドウマネージャ`awesome`の設定に書いています。


###<a name="p406">awesome</a>


次に、`awesome`の設定を見ていきます。ここは、設定ミスによって、ウィンドウマネージャが起動せず、混乱してしまうことがありますので、注意してください。

{% codeblock lang:bash %}
$ vim ~/.config/awesome/rc.lua
{% endcodeblock %}

変更する箇所としては、`dwb`と`editor`と`terminal`あたりです。


追記するのは、`xmodmap1`と`xmodmap2`ですね。


{% codeblock lang:lua ~/.config/awesome/rc.lua %}

-- 省略
terminal = "lilyterm"
editor = os.getenv("EDITOR") or "vim"
editor_cmd = terminal .. " -e " .. editor

-- Default modkey.
-- Usually, Mod4 is the key with a logo between Control and Alt.
-- If you do not like this or do not have such a key,
-- I suggest you to remap Mod4 to another key using xmodmap or other tools.
-- However, you can use another modifier like Mod1, but it may interact with others.
modkey = "Mod4"

-- 省略
    -- Applications
    awful.key({ modkey }, "[", function () awful.util.spawn_with_shell("xmodmap ~/.xmodmap1") end),
    awful.key({ modkey }, "]", function () awful.util.spawn_with_shell("xmodmap ~/.xmodmap2") end),
    awful.key({ modkey }, "d", function () awful.util.spawn_with_shell("firefox") end),
    awful.key({ modkey }, "t", function () awful.util.spawn_with_shell("spacefm") end)
)

{% endcodeblock %}


私はブラウザに`firefox`、ターミナルに`lilyterm`を設定しました。


また、先ほどのF1-F4までキーを切り替えするには、`Cmd+[`、`Cmd+]`を押します。


次に、壁紙でも変えてみることにします。

{% codeblock lang:bash %}
$ curl -O http://lh5.ggpht.com/-DBe6qOlsFVk/UxE1t1LosJI/AAAAAAAAH1U/lvVKxMKyifA/s0/arch_black.png

$ mv arch_black.png ~/.config/awesome/themes/cesious/

$ vim !$/theme.lua
{% endcodeblock %}

ここで、`background.jpg`の部分を`arch_black.png`に書き換えます。


反映させるには、`Mod4+Ctrl+r`を押し、awesomeを再起動します。


###<a name="p407">spacefm</a>

`spacefm`というのは、File Manager(ファイルマネージャ)です。デフォルトでは、`Mod4+t`で起動するはずです。


もし起動時にインストールしていない場合は、以下のコマンドでインストールできます。

{% codeblock lang:bash %}
$ sudo pacman -S spacefm
{% endcodeblock %}

右クリックの`View -> Hidden Files`ですべてのファイルを表示したり、`View -> Columns`で表示する項目を選択したり、`View -> Sort`で並び替えしたりできます。


なお、`nautilus`のほうが完成度が高いので、そちらの方もお勧めです。

{% codeblock lang:bash %}
$ sudo pacman -S nautilus

$ nautilus &
{% endcodeblock %}

###<a name="p408">firefox</a>

次に、`Firefox`の設定です。`vimperator`をインストールします。

`vimperator`についてですが、まずは、テーマもダウンロードしてきます。

{% codeblock %}
{% raw %}
$ cat << EOF > ~/.vimperatorrc
map j 5<C-e>
map k 5<C-y>
map a :bmark<cr>
noremap <C-b> :<C-b><esc><esc>
noremap <C-h> :<C-h><esc><esc>
complete=l
map ,b :bmarks!<space>
qmark g https://mail.google.com/
map B :bmarks! -tags
"read vimperatorrc
map S :source ~/.vimperator<cr>
EOF

$ curl https://raw.githubusercontent.com/tlync/vimperator-addons/master/colors/vimplight.vimp >> ~/.vimperatorrc
{% endraw %}
{% endcodeblock %}


さて、Manjaro Linuxもだいぶ便利になってきた感がありますが、ここからがカスタマイズの本番です。


###<a name="p409">lilyterm</a>

まずは、`lilyterm`の設定から行っていきましょう。


CUIから設定してもいいのですが、分かりやすいのは、GUIからの設定です。

{% codeblock lang:bash %}
$ lilyterm &
{% endcodeblock %}

起動後、右クリックで設定できます。

ちなみに、`lilyterm`は、設定したら、以下の項目を選択し、セーブする必要があります。



フォントは、`DejaVu Sans Mono`というものを使用しています。非常に良いフォントです。`powerline`との相性も良いです。




キーバインドは、`Tab operation`から`Add new tab`を変更したり、`Text operation`から`Copy to clipboard`、`Paste the text`を変更したりと最低限の設定をしておきましょう。



あとは、`Background`にて、ウィンドウの透過度を設定すると良いかもしれません。





一応、設定ファイルの編集方法を載せておきます。

{% codeblock lang:bash %}
$ vim ~/.config/lilyterm/default.conf
{% endcodeblock %}


###<a name="p410">zsh</a>

まずは、各種設定ファイルに必要なものをインストールします。


タイトル|URL
|---|---|
tmux-colors-solarized|https://github.com/seebi/tmux-colors-solarized
tmux-powerline|https://github.com/erikw/tmux-powerline
z|https://github.com/rupa/z
zaw|https://github.com/zsh-users/zaw
zsh-syntax-highlighting|https://github.com/zsh-users/zsh-syntax-highlighting
neobundle.vim|https://github.com/Shougo/neobundle.vim


{% codeblock lang:bash ~/install.sh %}

#!/bin/sh

git clone https://github.com/seebi/tmux-colors-solarized ~/dotfiles/.tmux/tools/tmux-colors-solarized
git clone https://github.com/erikw/tmux-powerline ~/dotfiles/.tmux/tools/tmux-powerline

git clone https://github.com/rupa/z ~/dotfiles/.zsh/tools/z
git clone https://github.com/zsh-users/zaw ~/dotfiles/.zsh/tools/zaw
git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/dotfiles/.zsh/tools/zsh-syntax-highlighting

git clone https://github.com/Shougo/neobundle.vim ~/.vim/bundle/neobundle.vim

{% endcodeblock %}


そして、`zsh`に最低限の設定をしてみました。


{% codeblock lang:bash %}
$ ./install.sh
{% endcodeblock %}

{% codeblock lang:bash ~/.zshrc %}
{% raw %}
autoload -U compinit colors zcalc
compinit
colors

setopt correct          # Auto correct mistakes
setopt extendedglob     # Extended globbing
setopt nocaseglob       # Case insensitive globbing
setopt rcexpandparam    # Array expension with parameters
setopt nocheckjobs      # Don't warn about running processes when exiting
setopt numericglobsort  # Sort filenames numerically when it makes sense
setopt nohup            # Don't kill processes when exiting
setopt nobeep           # No beep
setopt appendhistory    # Immediately append history instead of overwriting
setopt histignorealldups #If a new command is a duplicate, remove the older one

zstyle ':completion:*' matcher-list 'm:{a-zA-Z}={A-Za-z}'       # Case insensitive tab completion
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"         # Colored completion (different colors for dirs/files/etc)

bindkey -e
bindkey '^[[7~' beginning-of-line                   # Home key
bindkey '^[[8~' end-of-line                         # End key
bindkey '^[[2~' overwrite-mode                      # Insert key
bindkey '^[[3~' delete-char                         # Delete key
bindkey '^[[A'  up-line-or-history                  # Up key
bindkey '^[[B'  down-line-or-history                # Down key
bindkey '^[[C'  forward-char                        # Right key
bindkey '^[[D'  backward-char                       # Left key
bindkey '^[[5~' history-beginning-search-backward   # Page up key
bindkey '^[[6~' history-beginning-search-forward    # Page down key

HISTFILE=~/.zhistory
HISTSIZE=10000
SAVEHIST=10000

# ex - archive extractor
# usage: ex <file>
ex() {
  if [ -f $1 ] ; then
    case $1 in
      *.tar.bz2)   tar xjf $1   ;;
      *.tar.gz)    tar xzf $1   ;;
      *.bz2)       bunzip2 $1   ;;
      *.rar)       unrar x $1     ;;
      *.gz)        gunzip $1    ;;
      *.tar)       tar xf $1    ;;
      *.tbz2)      tar xjf $1   ;;
      *.tgz)       tar xzf $1   ;;
      *.zip)       unzip $1     ;;
      *.Z)         uncompress $1;;
      *.7z)        7z x $1      ;;
      *)           echo "'$1' cannot be extracted via ex()" ;;
    esac
  else
    echo "'$1' is not a valid file"
  fi
}

# prompt
#PROMPT="[%n@%m %1~] "
#RPROMPT="%{$fg[red]%}%(?..[%?])%{$reset_color%}"
source ~/dotfiles/.zsh/.zshrc.prompt

# open
alias open="xdg-open"
#alias open="gnome-open"
#alias open="cygstart"

# alias
alias sudo='sudo '
alias ls='ls --group-directories-first --time-style=+"%d.%m.%Y %H:%M" --color=auto -F'
alias ll='ls -l --group-directories-first --time-style=+"%d.%m.%Y %H:%M" --color=auto -F'
alias la='ls -la --group-directories-first --time-style=+"%d.%m.%Y %H:%M" --color=auto -F'
alias grep='grep --color=tty -d skip'
alias cp="cp -i"                        # Confirm before overwriting something
alias df='df -h'                        # Human-readable sizes
alias free='free -m'                    # Show sizes in MB

alias zs="vim ~/.zshrc"
alias zr="exec $SHELL"
alias vs="vim ~/.vimrc"
alias vr="vim +so $VIMRC"
alias ts="vim ~/.tmux.conf"
alias tmux="tmux -2"
alias ls='ls --color=auto -a'
alias ll="ls -slhAF"
alias cp="cp -v"
alias mv-all="mv */* . && rmdir * > /dev/null 2>&1"

# zaw
source $HOME/dotfiles/.zsh/tools/zaw/zaw.zsh

# mkcd
# http://d.hatena.ne.jp/yarb/20110126/p1
function mkcd() {
if [[ -d $1 ]]; then
echo "It already exsits! Cd to the directory."
cd $1
else
echo "Created the directory and cd to it."
mkdir -p $1 && cd $1
fi
}

# pbcopy-buffer
# http://d.hatena.ne.jp/hiboma/20120315/1331821642
pbcopy-buffer(){
print -rn $BUFFER | xclip -i -selection clipboard
zle -M "xclip: ${BUFFER}"
}
zle -N pbcopy-buffer
bindkey '^p^p' pbcopy-buffer

#google-search
function google-search() {
local str opt
if [ $ != 0 ]; then
for i in $*; do
str="$str+$i"
done
str=`echo $str | sed 's/^\+//'`
opt='search?num=50&hl=ja&lr=lang_ja'
opt="${opt}&q=${str}"
fi
w3m http://www.google.co.jp/$opt
}

# complete
autoload -U compinit
compinit
zstyle ':completion:*:default' menu select=2
zstyle ':completion:*' verbose yes
zstyle ':completion:*' completer _expand _complete _match _prefix _approximate _list _history
zstyle ':completion:*:messages' format '%F{YELLOW}%d'$DEFAULT
zstyle ':completion:*:warnings' format '%F{RED}No matches for:''%F{YELLOW} %d'$DEFAULT
zstyle ':completion:*:descriptions' format '%F{YELLOW}completing %B%d%b'$DEFAULT
zstyle ':completion:*:options' description 'yes'
zstyle ':completion:*:descriptions' format '%F{yellow}Completing %B%d%b%f'$DEFAULT
zstyle ':completion:*' list-separator '-->'
zstyle ':completion:*:manuals' separate-sections true
zstyle ':completion:*' group-name ''

# zaw
bindkey '^x^x' zaw
bindkey '^h' zaw-history

# cdpwd
function chpwd() { ls -aF }

# color
autoload colors
colors
source $HOME/dotfiles/.zsh/tools/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# code
export LANG=ja_JP.UTF-8

# tmux start
if [ -z "$TMUX" -a -z "$STY" ]; then
if type tmux >/dev/null 2>&1; then
if tmux has-session && tmux list-sessions | /usr/bin/grep -qE '.*]$'; then
tmux attach && echo "tmux attached session "
else
tmux new-session && echo "tmux created new session"
fi
fi
fi

# Android Mount
alias android="mkdir -p ~/Android && go-mtpfs ~/Android && lll || fusermount -u ~/Android"

# clipboard
if which pbcopy >/dev/null 2>&1 ; then
    # Mac
    alias -g C='| pbcopy'
elif which xclip >/dev/null 2>&1 ; then
    # Linux
    alias -g C='| xclip --input --clipboard'
elif which putclip >/dev/null 2>&1 ; then
    # Cygwin
    alias -g C='| putclip'
fi

# autojump
#export FPATH="$FPATH:/usr/share/zsh/site-functions/"
#[[ -s $HOME/.autojump/etc/profile.d/autojump.sh ]] && source $HOME/.autojump/etc/profile.d/autojump.sh

# z
source $HOME/dotfiles/.zsh/tools/z/z.sh
compctl -U -K _z_zsh_tab_completion ${_Z_CMD:-z}
alias j="z"
{% endraw %}
{% endcodeblock %}


ちなみに、`prompt`については、こちら。

{% codeblock lang:bash ~/dotfiles/.zsh/.zshrc.prompt %}
{% raw %}
# PROMPT {{{

setopt prompt_subst
setopt prompt_percent
setopt transient_rprompt

color256()
{
    local red=$1; shift
    local green=$2; shift
    local blue=$3; shift

    echo -n $[$red * 36 + $green * 6 + $blue + 16]
}

fg256()
{
    echo -n $'\e[38;5;'$(color256 "$@")"m"
}

bg256()
{
    echo -n $'\e[48;5;'$(color256 "$@")"m"
}

zstyle ':vcs_info:*' max-exports 3
zstyle ':vcs_info:hg:*' get-revision true
zstyle ':vcs_info:hg:*' use-simple true

autoload -Uz is-at-least
zstyle ':vcs_info:git:*' check-for-changes true
zstyle ':vcs_info:git:*' stagedstr "-"
zstyle ':vcs_info:git:*' unstagedstr "+"

zstyle ':vcs_info:git:*' formats '%K{green}%F{black}▶%k%f%%F{white}%K{green} %s %f%k%K{blue}%F{green}▶%k%f%%F{white}%K{blue} %b %f%k%K{black}%F{blue}▶%k%f%%F{white}%K{black} %c%u %f%k'

autoload -Uz vcs_info
prompt_bar_left_self="%{%F{white}%K{blue}%}  %n%{%k%f%}%{%F{white}%K{blue}%}@%{%k%f%}%{%F{white}%K{blue}%}%m %{%k%f%}%{%B%F{blue}%K{blue}%}%{%b%f%k%}%K{cyan}%F{blue}▶%k%f%{%B%F{white}%K{cyan}%}  [%~]  %{%k%f%b%}%{%k%f%}%K{red}%F{cyan}▶%k%f%(?.%F{white}%K{red}%}  COMP  %k%f.%B%K{red}%F{red}%}  ERROR  %b%k%f)%{%K{green}%F{red}▶%k%f%F{white}%K{green}%}  -%h  %{%k%f%}%K{black}%F{green}▶%k%f"

  #TMUX_POWERLINE_SEPARATOR_LEFT_BOLD="◀"
  #TMUX_POWERLINE_SEPARATOR_LEFT_THIN="❮"
  #TMUX_POWERLINE_SEPARATOR_RIGHT_BOLD="▶"
  #TMUX_POWERLINE_SEPARATOR_RIGHT_THIN="❯"

prompt_bar_left="${prompt_bar_left_self} ${prompt_bar_left_status} ${prompt_bar_left_date}"
prompt_left='%{%F{white}%K{black}%}  $SHELL  %{%k%f%}%{%K{white}%F{black}▶%k%f%B%F{black}%K{white}%} %# %{%b%k%f%f%}%K{black}%F{white}▶%k%f '

count_prompt_characters()
{
    print -n -P -- "$1" | sed -e $'s/\e\[[0-9;]*m//g' | wc -m | sed -e 's/ //g'
}

update_prompt()
{
    local bar_left_length=$(count_prompt_characters "$prompt_bar_left")
    local bar_rest_length=$[COLUMNS - bar_left_length]

    local bar_left="$prompt_bar_left"
    local bar_right_without_path="${prompt_bar_right:s/%d//}"
    local bar_right_without_path_length=$(count_prompt_characters "$bar_right_without_path")
    # local max_path_length=$[bar_rest_length - bar_right_without_path_length]
    bar_right=${prompt_bar_right:s/%d/%(C,%${max_path_length}<...<%d%<<,)/}
    bar_right="%${bar_rest_length}<<${separator}${bar_right}%<<"

    PROMPT="${bar_left}${bar_right}"$'\n'"${prompt_left}"

    RPROMPT="%K{white}%F{black}▶%k%f%{%F{black}%K{white}%} %l  %K{black}%F{white}▶%k%f%{%k%f%}%{%F{white}%K{black}%}  $LANG  %{%k%f%}"

    case "$TERM_PROGRAM" in
        Apple_Terminal)
            RPROMPT="${RPROMPT}"
            ;;
    esac

    LANG=C vcs_info >&/dev/null
    if [ -n "$vcs_info_msg_0_" ]; then
        RPROMPT="${vcs_info_msg_0_}${RPROMPT}"
    fi
}

precmd_functions=($precmd_functions update_prompt)

# }}}
{% endraw %}
{% endcodeblock %}

###<a name="p411">vim</a>

`vim`の最低限の設定をしてみました。といっても、主に見た目を変えているだけですが。


ただし、中には、`+lua`でないと動作しないプラグインもあります。そういう時は、vimを再コンパイルするか、`gvim`をインストールしてくださいな。

{% codeblock lang:bash %}
$ sudo pacman -S gvim
{% endcodeblock %}


{% codeblock lang:vim ~/.vimrc %}
{% raw %}
if has('vim_starting')
   set nocompatible               " Be iMproved
   set runtimepath+=~/.vim/bundle/neobundle.vim/
 endif

 call neobundle#rc(expand('~/.vim/bundle/'))

 " Let NeoBundle manage NeoBundle
 NeoBundleFetch 'Shougo/neobundle.vim'

 " Recommended to install
 NeoBundle 'Shougo/vimproc', {
  \ 'build' : {
  \     'windows' : 'make -f make_mingw32.mak',
  \     'cygwin' : 'make -f make_cygwin.mak',
  \     'mac' : 'make -f make_mac.mak',
  \     'unix' : 'make -f make_unix.mak',
  \    },
  \ }

NeoBundle "Shougo/unite.vim"
NeoBundle "Shougo/neosnippet.vim"
NeoBundle "Shougo/neosnippet-snippets"
NeoBundle "Shougo/vimfiler.vim"
NeoBundle "Shougo/neocomplete.vim"
NeoBundle "kana/vim-textobj-user"
NeoBundle "tpope/vim-surround"
NeoBundle "syui/airsave.vim"
NeoBundle "osyo-manga/vim-over"
NeoBundle "sudo.vim"
NeoBundle "Lokaltog/vim-easymotion"
NeoBundle "rhysd/clever-f.vim"
NeoBundle "Lokaltog/vim-powerline"

" color theme
NeoBundle 'nanotech/jellybeans.vim'
NeoBundle 'w0ng/vim-hybrid'
NeoBundle 'vim-scripts/twilight'
NeoBundle 'jonathanfilip/vim-lucius'
NeoBundle 'jpo/vim-railscasts-theme'
NeoBundle 'altercation/vim-colors-solarized'
NeoBundle 'vim-scripts/Wombat'
NeoBundle "tomasr/molokai"
NeoBundle "vim-scripts/rdark"
filetype plugin indent on
NeoBundleCheck

" keymap
inoremap <silent><C-j> <ESC>
inoremap <silent>jj <ESC>
nmap <C-p> "*p
nmap Q :q!<CR>

" color
colorscheme molokai
syntax on
set t_Co=256

" clipboard
set clipboard=unnamedplus,unnamed

" swap
set noswapfile

" number
set number

" encode
set encoding=utf-8

"vim-over
nnoremap <silent> <C-n> :OverCommandLine<CR>%s/

" airsave.vim
nmap <Leader>s  <Plug>(AutoWriteStart)
nmap <Leader>ss <Plug>(AutoWriteStop)
let g:auto_write = 1

" easymotion
let g:EasyMotion_keys='hjklasdfgyuiopqwertnmzxcvb'
let g:EasyMotion_leader_key=";"
let g:EasyMotion_grouping=1

" powerline
set laststatus=2
let g:Powerline_symbols = 'unicode'
{% endraw %}
{% endcodeblock %}


###<a name="p412">tmux</a>

`tmux`の最低限の設定を自分なりに考えてみました。

{% codeblock lang:bash ~/.tmux.conf %}
{% raw %}
set-option -g status on
set-option -g status-interval 2
set-option -g status-utf8 on
set-option -g status-justify "centre"
set-option -g status-left-length 60
set-option -g status-right-length 90
set-option -g status-left "#(~/dotfiles/.tmux/tools/tmux-powerline/powerline.sh left)"
set-option -g status-right "#(~/dotfiles/.tmux/tools/tmux-powerline/powerline.sh right)"

bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
bind H resize-pane -L 5
bind J resize-pane -D 5
bind K resize-pane -U 5

set -g status on
set -g status-utf8 on

# Color
# set-option -g default-terminal "screen-256color"
#### COLOUR (Solarized 256)

unbind r
bind r source-file ~/.tmux.conf

# default statusbar colors
set-option -g status-bg colour235 #base02
set-option -g status-fg colour136 #yellow
set-option -g status-attr default

# default window title colors
set-window-option -g window-status-fg colour244 #base0
set-window-option -g window-status-bg default
#set-window-option -g window-status-attr dim

# active window title colors
set-window-option -g window-status-current-fg colour166 #orange
set-window-option -g window-status-current-bg default
#set-window-option -g window-status-current-attr bright

# pane border
set-option -g pane-border-fg colour235 #base02
set-option -g pane-active-border-fg colour240 #base01

# message text
set-option -g message-bg colour235 #base02
set-option -g message-fg colour166 #orange

# pane number display
set-option -g display-panes-active-colour colour33 #blue
set-option -g display-panes-colour colour166 #orange

# clock
set-window-option -g clock-mode-colour colour64 #green

# Use vim keybindings in copy mode
setw -g mode-keys vi

# prefix key
# Set the prefix to ^T.
unbind C-b
set -g prefix ^T
bind t send-prefix

# clipboard = xclip
#bind C-c run "tmux show-buffer | xclip -i -selection clipboard"
bind C-c run "tmux choose-buffer | xclip -i -selection clipboard"

# [p]paste
bind p paste-buffer

# [cEnter]copy select
bind -t vi-copy Enter copy-selection
bind-key -t vi-copy Enter copy-pipe "xclip -i -selection clipboard"
# [cY]copy 1 line
bind -t vi-copy Y select-line

# [y]copy 1 line
#bind y run 'tmux copy-mode\; send-keys Y Enter'
bind y run 'tmux copy-mode\; send-keys Y'

bind -t vi-copy V begin-selection
# [v]copy all
bind v run 'tmux copy-mode\; send-keys ggVG Enter'

# http://d.hatena.ne.jp/naoya/20130108/1357630895
bind C-t run "tmux last-pane || tmux last-window || tmux new-window"

# end
bind K kill-pane
{% endraw %}
{% endcodeblock %}

`prefix`を`t`に変更したので、`C-b`ではなく、`C-t`となります。


ちょっと`tmux-powerline`の`ifstat`が動作しませんので、Linux用のスクリプトを書いてみました。

{% codeblock lang:bash ~/dotfiles/.tmux/tools/tmux-powerline/segments/ifstat.sh %}
#!/bin/sh
# Show network statistics for all active interfaces found.

run_segment() {
rx=`ifstat -j | jq '.kernel[].rx_bytes' | head -n 1`
tx=`ifstat -j | jq '.kernel[].tx_bytes' | head -n 1`
rx=`expr $rx / 10000000`
tx=`expr $tx / 10000000`
ifs=$(echo "⇊ 0.${rx} ⇈ 0.${tx}")
echo $ifs
}
{% endcodeblock %}

上手くいかない場合は、割り算、`expr $tx / 10000000`の値でも変更してみましょう。


元のスクリプトを残しておきたい場合は、OSを判断する処理を書きます。


###<a name="p413">Manjaro LinuxをMacの仮想環境上で動作させる方法</a>


####Virtual Manjaro Linuxの初期設定

仮想環境として直にインストールする場合と比較し、異なる部分としては、まず、ブートローダーの設定にて、`BIOS`を選択します。




あとは、`awesome`の`modkey = "Mod1"`くらいでしょうか。

{% codeblock lang:bash %}
$ sed -ie 's/Mod4/Mod1/g' ~/.config/awesome/rc.lua
{% endcodeblock %}

この設定は、`Cmd`を`Alt`に変更するものです。


####<a name="network">ホストOSからゲストOSへのSSH接続を可能にする</a>

その他、SSH接続に関して説明します。具体的には、以下の様な接続を確立します。


> ホストOSからゲストOSへのSSH接続を可能にする

> 外部(WAN)からゲストOSへの接続を制限する

> ゲストOSから外部(WAN)への接続を許可する


これは、主に、ホストOSからのリモートアクセスのみを可能にする設定です。


この場合、ホストは、Mavericksです。ゲストは、Manjaro Linuxです。


まず、`VirtualBoX`の設定ですね。`Cmd+,`を押して、VirtualBoxのネットワーク設定を行います。具体的には、`NATネットワーク`、`ホストオンリーネットワーク`に設定を追加します。追加する項目は、デフォルトでいいでしょう。設定には、DNSなども含まれるため、アドレスを固定したい場合などは、適時変更してください。





次に、ゲストOSのネットワーク設定です。簡単には、ゲストOSのネットワーク設定でアダプタ1を`NAT`、`準仮想化ネットワーク`にします。次に、アダプタ2で`ホストオンリーアダプター`、`準仮想化ネットワーク`にします。




設定を終えたら、ホストからゲストに通信ができるかを確認してみましょう。


まずは、LAN Address(アドレス)の確認からですね。基本的に、Arch Linuxには`ifconfig`が入ってないので、インストールしておきましょう。


{% codeblock lang:bash ゲストOS %}
$ sudo pacman -S net-tools openssh

$ ifconfig

$ ifconfig | tr ' ' '\n' | grep 192
{% endcodeblock %}

{% codeblock lang:bash ホストOS %}
$ ping 192.168.56.101
{% endcodeblock %}

では、次に、SSH Server(サーバー)の設置と、場合によっては、Firewall(ファイアウォール)の設定を変更しなければなりません。


具体的には、SSH ServerをDaemon(デーモン)で起動し、サーバーに設定した接続ポートへのアクセスをFirewallに許可させなければなりません。


SSH Serverの設定を変更します。ここでは、デフォルトのままで良いです。変更したい方は、変更して下さい。

{% codeblock lang:bash %}
# setting
$ sudo vim /etc/ssh_config

# SSH Serverを起動します。
$ sudo systemctl start sshd

# SSH Serverを起動時に有効にします。
$ sudo systemctl enable sshd.service
{% endcodeblock %}



では、ホストOSからゲストOSのSSH Serverに接続してみましょう。

{% codeblock lang:bash SSH %}
$ ssh manjaro@192.168.56.101
{% endcodeblock %}

といっても、このままのサーバー設定では非常に危険ですので、練習のためにもSSH Server、Firewallの設定を変更してみましょう。まあ、VirtualBoxの設定で一応安全な設定を選択してますが。


公開鍵の発行と受け渡しです。

{% codeblock lang:bash クライアント %}
$ ssh-keygen -t rsa

$ brew install ssh-copy-id

$ ssh-copy-id -i ~/.ssh/id_rsa.pub manjaro@192.168.56.101
{% endcodeblock %}

サーバー側の設定を変更します。最低限のセキュリティを強化します。

{% codeblock lang:bash /etc/ssh/sshd_config %}
Port 55010

RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile  .ssh/authorized_keys

PasswordAuthentication no
{% endcodeblock %}


SShデーモンの再起動は以下のコマンドを実行します。

{% codeblock lang:bash %}
$ sudo systemctl restart sshd
{% endcodeblock %}

接続は、以下の様な感じで行えます。

{% codeblock lang:bash %}
$ ssh manjaro@192.168.56.101 -p 55010
{% endcodeblock %}

Firewallを有効にし、ステータスを確認します。

{% codeblock lang:bash Firewall %}
# 有効
$ sudo ufw enable

# ローカルネットワーク(192.168.56.1-3)からの特定のポートへの接続を許可
$ sudo ufw allow proto tcp from 192.168.56.1 to any port 22
$ sudo ufw allow proto tcp from 192.168.56.1 to any port 55010

# ステータス
$ sudo ufw status

# Firewallをデーモンで起動する
$ sudo systemctl start ufw
$ sudo systemctl enable ufw
{% endcodeblock %}


ちなみに、アドレスの固定方法ですが、VirtualBoxの設定からの方法が最も簡単です。

> ネットワーク -> ホストオンリーネットワーク

> vboxnet0, vboxnet1, vboxnet2 のように複数作成します。

> 各自アドレスを変更します。ゲストのアドレスは、ホストのアドレスと合わせてください。

> 先ほど設定したホストオンリーネットワークのvboxnet"n"を各種OSのネットワーク設定に指定します。








{% codeblock lang:bash 例 %}
# Arch Linux
アダプタ: 192.168.56.1, DHCPサーバー: 192.168.56.101

# Windows
アダプタ: 192.168.57.1, DHCPサーバー: 192.168.57.101

# CentOS
アダプタ: 192.168.58.1, DHCPサーバー: 192.168.58.101
{% endcodeblock %}


この設定により、接続コマンドを固定できます。


<a href="https://wiki.archlinux.org/index.php/Secure_Shell_(%E6%97%A5%E6%9C%AC%E8%AA%9E)" target="_blank">Secure Shell (日本語) - ArchWiki</a>

<a href="https://wiki.archlinux.org/index.php/Uncomplicated_Firewall" target="_blank">Uncomplicated Firewall - ArchWiki</a>


相変わらず、[Arch Wiki](https://wiki.archlinux.org/)の充実度はすごい...。


私が Arch ないしは、 Arch 派生のOSを好んで使用する主な理由は、このWikiが理由の一つだったりします。


##Linux | Kail Linux

|Kail Linux|
|---|
|[Kail Linxuで使っているアプリ](#p500)

###<a name="p500">Kail Linuxで使っているアプリ</a>

####[MetaSploit](http://www.metasploit.com/)

脆弱性関連の基本情報は[こちら](http://www.ibm.com/developerworks/jp/web/library/wa-metasploit/)で確認できます。このアプリは、Exploitの中核、または最終段階で使用されることが多いアプリです。また、様々なアプリとの連携を可能にします。

####[Aircrack-ng](http://www.aircrack-ng.org/)

無線LANのパスワードをクラックできるアプリです。まずパケットを集め、時間をかけて予想されるパスワードを組み合わせていきます。

####[WireShark](http://www.wireshark.org/)

パケット解析アプリです。ネットワーク情報は、パケットを解析することで明らかになります。

####[Nmap](http://nmap.org/man/jp/)

ネットワークスキャンアプリ。主に、WAN上の不明確なネットワークをスキャンするために使用されます。Exploitの初期段階で使用されることが多いアプリです。

####[Ophcrack](http://ophcrack.sourceforge.net/)

定番のパスワードクラックアプリです。パスワードクラックには、辞書による解読よりも、分散処理によるブルートフォースが有効になりつつある今日です。そのため、セキュリティ強化には、アタックするための回数を制限する処置が必須。


##Tips | おまけ

###cygstart

`cygstart`はmacでいう`open`のようなものです。

{% codeblock lang:bash cygwinにwgetとcurlをインストール %}
$ cygstart /cygdrive/c/Cygwin/cygwinsetup -q -P wget, curl
{% endcodeblock %}

ちなみに、Linuxの場合は、以下の様なコマンドが使えます。

{% codeblock lang:bash 現在のディレクトリをファイルマネージャーで開く %}
$ xdg-open .

$ gnome-open .
{% endcodeblock %}


###ssh-copy-id

{% codeblock lang:bash 公開鍵をサーバー側に渡します %}
$ ssh-keygen -t rsa

$ brew install ssh-copy-id

$ ssh-copy-id -i ~/.ssh/id_rsa.pub username@192.168.56.101
{% endcodeblock %}


###openssh

sshは高速化することができます。[mosh](http://mosh.mit.edu/)を使っても良いです。

{% codeblock lang:bash /etc/ssh/ssh_config %}
Host examplehost.com
  ControlMaster auto
  ControlPersist yes
  ControlPath ~/.ssh/socket-%r@%h:%p
  Compression yes
  AddressFamily inet
{% endcodeblock %}


###ifconfig

{% codeblock lang:bash %}
$ ifconfig | tr ' ' '\n' | grep 192
{% endcodeblock %}


{% codeblock lang:bash グローバルIPアドレスを表示する http://qiita.com/hyone/items/8b7132c8f0d8c8f53f40 LINK %}
$ curl -s ipinfo.io | jq -r .ip

$ curl ifconfig.me
{% endcodeblock %}


###lilyterm

Linuxでのターミナルアプリは、`lilyterm`がおすすめです。

{% codeblock lang:bash %}
$ sudo pacman -S lilyterm
{% endcodeblock %}

###gvim

`if_lua`を有効にするには、再コンパイルするか、`gvim`でもインストールしてくださいな。

{% codeblock lang:bash %}
$ sudo pacman -S gvim
{% endcodeblock %}

###make

Cygwinでは、ビルドが遅いらしいが、コアを使うことにより改善されます。

{% codeblock lang:bash %}
$ time make -j2
{% endcodeblock %}

###posh-git

同様、Windowsでは、`git`が遅いですが、以下の設定により改善されます。ちなみに、[posh-git](https://github.com/dahlbyk/posh-git)を使います。

{% codeblock lang:bash powershell_profile.ps1 %}
$GitPromptSettings.EnableFileStatus = $false
{% endcodeblock %}

###Sysinternals Suite

Windowsでは、[Sysinternals Suite](http://technet.microsoft.com/ja-jp/sysinternals/bb842062.aspx)が特に使えます。




