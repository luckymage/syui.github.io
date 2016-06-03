---
layout: post
title: "zshでのディレクトリ移動、上と下"
date: 2014-09-06
comments: true
categories: [ shell ]
tags: [ zsh ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">上に移動するキーと下に移動するキーを設定します。<!--more--><br clear="all">

上のキーは簡単ですが、下のキーは割りと変更しています。今度は、`peco`使うことにしました。

{% codeblock lang:bash ~/.zshrc %}
{% raw %}
# C-kで上のディレクトリ移動
function cdup_dir() {
  if [[ -z "$BUFFER" ]]; then
    echo
    cd ..
    ls -aF
    zle reset-prompt
  else
    zle self-insert 'k'
  fi
 }
zle -N cdup_dir
bindkey '^k' cdup_dir

# C-jで下のディレクトリ移動(peco)
function cddown_dir(){
com='zsh -c "ls -AF . | grep / "'
while [ $? = 0 ]
do
    cdir=`eval $com | peco`
    if [ $? = 0 ];then
        cd $cdir
        eval $com
    else
        break
    fi
done
zle reset-prompt
}
zle -N cddown_dir
bindkey '^j' cddown_dir
{% endraw %}
{% endcodeblock %}

`ls`は、エイリアス設定してる場合も多いので、`zsh -c`を付けます。設定なしで実行です。

