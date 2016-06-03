---
layout: post
title: "まともなアニメの感想記事がヒットしない件"
date: 2014-10-14
comments: true
categories: [blog, anime]
tags: middleman, slim, sass, bootstrap
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">私もたまにアニメの感想とか読みたいな思って、検索することがあるのですが、まともなサイトが全くヒットしないので、困っています。<!--more--><br clear="all">

`ごちうさ感想`でGoogle検索し、10ページ以内にあったまともな記事は、たった2つでした。

<a href="http://d.hatena.ne.jp/tanami/20140719/1405769545" target="_blank">『ご注文はうさぎですか？』感想。 - ぱっしょん</a>

<a href="http://globalpeacecommunication.blogspot.jp/2014/07/blog-post_8.html" target="_blank">Clap your Sunday!: ご注文はうさぎですか？　を考える。感想。</a>

後は、`まとめサイト`か`FC2`かどちらかという感じでした。FC2は、広告が凄くてあまり好きではないので除きました。また、文字数が極端に少ない場合も除外しています。

スマホでも苦もなく読めて、かつ自分好みのアニメ感想サイトがなかなか見つかりません。

よって、作ってみることにしました。使ったのは、以下の様なものです。良さそうな[テンプレート](https://github.com/biblichor/middleman-blog-bootstrap-template)が公開されていたので、それを参考にしました。

{% githubrepo biblichor/middleman-blog-bootstrap-template %}

- [middleman-blog](https://github.com/middleman/middleman-blog/)

- [bower](https://github.com/bower/bower)

- [slim](http://slim-lang.com/)

- [markdown](http://daringfireball.net/projects/markdown/)

- [sass](http://sass-lang.com/)

実際、サイトを立ち上げるまでは一瞬でできます。

{% codeblock lang:bash %}
$ gem install middleman

$ git clone https://github.com/biblichor/middleman-blog-bootstrap-template.git ~/.middleman/blog-bootstrap

$ middleman init my_new_project --template=blog-bootstrap

$ cd my_new_project

$ bower install
{% endcodeblock %}

こんな感じで必要な物をインストールして、後は設定ファイルを書いて、

{% codeblock lang:bash my_new_project/config.rb %}
{% raw %}
# Build-specific configuration
configure :build do
  #activate :gzip
  activate :minify_css
  activate :minify_javascript
  activate :asset_host, :host => "/my_new_project"
  activate :asset_hash
  set :relative_links, true
end

activate :deploy do |deploy|
  deploy.build_before = true
  deploy.method = :git
  deploy.branch = 'gh-pages'
end
{% endraw %}
{% endcodeblock %}

デプロイするだけです。

`$ middleman deploy`

しかし、調整には結構面倒でした。`slim`を書き始めたばかりというのや、そもそも`bootstrap`のカスタマイズをあまり分かってないことが大きかったです。

とりえず、時間がかかったところだけ紹介します。

{% codeblock lang:html %}
{% raw %}
/! 記事全体にエフェクト
- page_articles.each_with_index do |article, i|
  .article-o [onclick="location.href=&#34;.#{article.url}&#34;;" style="cursor: pointer;"]

/! アイキャッチ画像
img[width="600" height="300" id="img-responsive" src=article.data.image_src]

/! なんか知らないけど、タグだけリンクが動作しなかったので、その対応(root urlの/animeを追加)
.well
  h4 アニメ一覧
  ul.list-unstyled
    - blog.tags.each do |tag, articles|
      li
        = link_to tag, "/anime#{tag_path(tag)}"
        |  (
        = articles.size
        | )
{% endraw %}
{% endcodeblock %}

一番最後のリンクが動作しない奴は、多分、`GitHub Pages`のプロジェクトページを使っていることが原因だと思われます。設定で対応できそうだけど、分からなかったので、強引にURLを修正して対応しました。

あとは、CSS周りも。特にモバイル対応ですが、ちょっとよく分からなかったです。iPhoneで確認したのですが、前、Middleman触った時とだいぶフォントサイズが違うので。`20px -> 35px`にしないと、小さい感じになってしまう。

{% codeblock lang:css bower_components/sass-bootstrap/lib/_variables.scss %}
// Extra small screen / phone
// Note: Deprecated $screen-xs and $screen-phone as of v3.0.1
$screen-xs:                  480px !default;
$screen-xs-min:              $screen-xs !default;
$screen-phone:               $screen-xs-min !default;

// Small screen / tablet
// Note: Deprecated $screen-sm and $screen-tablet as of v3.0.1
$screen-sm:                  992px !default;
$screen-sm-min:              $screen-sm !default;
$screen-tablet:              $screen-sm-min !default;

// Medium screen / desktop
// Note: Deprecated $screen-md and $screen-desktop as of v3.0.1
$screen-md:                  992px !default;
$screen-md-min:              $screen-md !default;
$screen-desktop:             $screen-md-min !default;

$font-size-base:          16px !default;
$font-size-large:         ceil($font-size-base * 1.25) !default; // ~18px
$font-size-small:         ceil($font-size-base * 1.0) !default; // ~12px

$font-size-h1:            floor($font-size-base * 2.6) !default; // ~36px
$font-size-h2:            floor($font-size-base * 2.15) !default; // ~30px
$font-size-h3:            ceil($font-size-base * 1.7) !default; // ~24px
$font-size-h4:            ceil($font-size-base * 1.25) !default; // ~18px
$font-size-h5:            $font-size-base !default;
$font-size-h6:            ceil($font-size-base * 0.85) !default; // ~12px
{% endcodeblock %}

フォントサイズとか一括設定があって、便利。

{% codeblock lang:css source/css/_mobile.scss %}
@media screen and (max-width: 992px) {

  body {
    font-size: 35px;
  }

  .container {
    margin-right: 0;
    margin-left: 0;
    padding-left: 0;
    padding-right: 0;
  }

  .col-lg-3.col-md-3 {
    padding-left: 4;
    padding-right: 4;
  }
  .col-lg-9.col-md-9 {
    padding-left: 4;
    padding-right: 4;
  }

}
{% endcodeblock %}

ここで、アニメブログの方針としては、自分が読みたい感想を書く感じでやってくつもりです。具体的には、①BD、OP、CMとかの情報、②好きなキャラとキャラ解説、③物語の評価という感じです。

目次とかアマゾンとかもそのうち付けられれば付けるかもしれません。

https://github.com/AknEp/middleman-toc-sample

https://github.com/andrusha/middleman-cloudfront

