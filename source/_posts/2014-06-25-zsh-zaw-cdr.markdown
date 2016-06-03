---
layout: post
title: "zshのzawを使ったディレクトリ移動とファイルの実行"
date: 2014-06-25
comments: true
categories: [terminal]
tags: [zsh, shell, zaw, mac, cdr]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">zsh に追加された cdr を使います。<!--more--><br clear="all">

私の場合は、`z hoge<Tab>`または、`Ctrl+jj`でディレクトリ移動をしています。前者は[z](https://github.com/rupa/z)を使います。後者は[zaw](https://github.com/zsh-users/zaw)です。

あと、ファイルを開く動作は、`Ctrl+o`、`Ctrl+oo`です。前者は`Application`を検索します。後者は`vim`で開きます。

ちなみに、プロンプトに何のコマンドが実行されたのかの表示を残したい場合は、`bindkey -s{v, e}`を使いましょう。

{% codeblock lang:bash ~/.zshrc %}
{% raw %}
# z {{{
# brew install z
. `brew --prefix`/etc/profile.d/z.sh
compctl -U -K _z_zsh_tab_completion ${_Z_CMD:-z}
# }}}

# cdr {{{
autoload -Uz chpwd_recent_dirs cdr add-zsh-hook
zstyle ':completion:*:*:cdr:*:*' menu selection
zstyle ':completion:*' recent-dirs-insert both
zstyle ':chpwd:*' recent-dirs-max 500
zstyle ':chpwd:*' recent-dirs-default true
zstyle ':chpwd:*' recent-dirs-pushd true
# }}}

# zaw-cdr
# git clone https://github.com/zsh-users/zaw
# source /path/to/zaw.zsh
bindkey '^j^j' zaw-cdr

# percol-open-vim
# git clone https://github.com/mooz/percol
# sudo python setup.py install
bindkey -sv '^o^o' 'vim $(ls | percol)\n'

# mac-open-application {{{
case "${OSTYPE}" in
# MacOSX
darwin*)
  function openapp() {
    BUFFER="open -a "
    CURSOR=$#BUFFER
  }
  zle -N openapp
  bindkey '^o' openapp
;;
esac
# }}}

# open-commmand {{{
case "${OSTYPE}" in
freebsd*|darwin*)
    alias o="open"
    ;;
linux*)
    alias open="xdg-open"
    #alias open="gnome-open"
cygwin*)
    alias open="cygstart"
    ;;
esac
# }}}
{% endraw %}
{% endcodeblock %}

こんな感じで、[percol](https://github.com/mooz/percol)を使うことも多いのですが、[zaw](https://github.com/zsh-users/zaw)も使います。

印象ですが、`percol`はシンプルな設計で、非常に組み込みやすいため、自作ツールのインターフェイスとして利用する場面が多く、`zaw`は、普段使いと言った感じで利用する場面が多いです。

ちなみに、 zaw で z の history を使用したい場合は、以下のプラグインを使いましょう。

{% codeblock lang:bash %}
{% raw %}
$ cd /path/to/zaw/source

$ curl -O https://raw.githubusercontent.com/lovingly/dotfiles/master/zsh.d/zaw/zaw-z.zsh

$ echo "bindkey '^f^f' zaw-z" >> ~/.zshrc
{% endraw %}
{% endcodeblock %}


