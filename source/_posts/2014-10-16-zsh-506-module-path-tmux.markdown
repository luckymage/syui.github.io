---
layout: post
title: "zsh-5.0.6にアップデートしたらtmux起動時にパスがおかしくなった"
date: 2014-10-16
comments: true
categories: shell
tags: [ zsh, tmux ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">tmuxとか起動すると、`$module_path`が前のバージョンのものになっている件について<!--more--><br clear="all">

> どうやら/etc/zshenvで実行されるpath_helperが変なことやっているようです。

ということで、以下の設定で対応できます。

{% codeblock lang:bash ~/.zshrc %}
if [ -x /usr/libexec/path_helper ]; then
    eval `/usr/libexec/path_helper -s`
fi
export PATH=${HOME}/local/bin:${HOME}/bin:/usr/local/bin:$PATH
{% endcodeblock %}

参考:

<a href="http://hayajo.tumblr.com/post/12281915216/osx-zsh-path" target="_blank">hayajoのTumblr, OSXでのzshにおけるPATH設定</a>

<a href="https://github.com/yosida95/dotfiles/blob/master/README.md" target="_blank">dotfiles/README.md at master · yosida95/dotfiles</a>

