---
layout: post
title: "Google+との連携を考える"
date: 2014-06-03
comments: true
categories: [blog]
tags: [api, octopress, google, github, sns]
---


<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">ブログとGoogle+の連携を考えます。また、Google+ページのカスタムURLについても少しだけ紹介します。<!--more--><br clear="all">


##Google+のカスタムURL

Google+では、カスタムURLを取得することができます。

ここで、条件を満たせば、以下のようなURLを取得したりすることができます。

`https://plus.google.com/+syui/`

カスタムURLは、個人ページと作成ページで取得することができます。

個人ページのカスタムURLは、姓名が使われます。

反対に、作成ページでは、リンクしたウェブサイトのURLが使われます。ここで、ドメインが`.com`の場合は、これが省略されるみたいです。

作成ページでのカスタムURLは、以下の条件で取得できるようになります。

> **ユーザーの利用資格：**
>
>   フォロワーが10人以上いる
>
>   アカウントを30日以上利用している
>
>   プロフィール写真（デフォルトではないことか？[未確認]）
>
> **Google+ローカルページの利用資格：**
>
> 確認済みのローカルビジネスであること
>
> **Google+ローカルページ以外の利用資格：**
>
> ウェブサイトにリンクしていること


作成ページでのカスタムURLは、原則、リンクしたウェブサイトのドメインが使用されます。

例えば、以下のページのURLを見てください。

<a href="https://plus.google.com/+kaguabiz/" target="_blank">+kaguabiz</a>

<a href="https://plus.google.com/+Monochrome-photoinfo/" target="_blank">+Monochrome-photoinfo</a>

ここで、URLには、`.biz`や`.info`が末尾に追加されています。なぜなら、ウェブサイトのURLが`www.kagua.biz`だからです。

しかし、`.com`を使うことで、ドメインを省略することができるようです。例えば、以下のページを見てください。

<a href="https://plus.google.com/+Appllio/" target="_blank">+Appllio</a>

<a href="https://plus.google.com/+Plus1world/" target="_blank">+Plus1world</a>

ここで、リンクしているウェブサイトのURLは、`appllio.com`です。

他にもドメインの部分を省略できるものがあるかもしれません。考えられるものとしては、`.net`などでしょうか。

また、[gplus.to](http://gplus.to/)という短縮URLにしてくれるウェブサービスも存在します。


###追記

####.org

`.org`でもカスタムURLのドメイン部分の省略を確認しました。

<a href="https://plus.google.com/+Kiva" target="_blank">https://plus.google.com/+Kiva</a>


##検索結果

Google+とブログを連携することで、ブログ関連の記事を対象にした検索結果に影響をおよぼすことができます。


###アイコン

Google+とブログを連携することで、ブログ関連のページを対象にした検索結果にアイコンが表示されるようになります。


ただし、プロフィール写真で顔認識がオンになってる必要があります(タグ付け)。

関連付けは、以下のタグを使います。

`rel=author`

{% codeblock lang:html 例 %}
{% raw %}
<a href="http://syui.github.io/" rel="author"></a>
{% endraw %}
{% endcodeblock %}

###右サイド

Google+ページとブログを連携することで、ブログ関連のページを対象にした検索結果の左サイドに、ブログと関連付けたGoogle+ページが表示されるようになります。


まず、当該Google+ページをフォローしている人に、表示される事が多いです。

次に、ブログが一定のアクセス数に達していれば、フォローしているか否かに関係なく表示されることが多いです。

関連付けは、以下のタグを使います。

`rel=publisher`

{% codeblock lang:html 例 %}
{% raw %}
<a href="http://syui.github.io/" rel="publisher"></a>
{% endraw %}
{% endcodeblock %}

###Google+ページ

検索結果には、フォローしているGoogle+ページがアイコン付きで表示されることがあります。


参考:

<a href="https://support.google.com/plus/answer/1151728?hl=ja" target="_blank">プロフィールの検索結果設定の変更</a>

<a href="https://support.google.com/plus/answer/2676340?hl=ja" target="_blank">Google+ カスタム URL スタート ガイド</a>
