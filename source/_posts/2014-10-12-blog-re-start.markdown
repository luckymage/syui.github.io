---
layout: post
title: "HTMLを書く気がしなかったので、Slimを使ってみた"
date: 2014-10-12
comments: true
categories: programming
tags: [ html, slim ]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Slimを使ってみました。<!--more--><br clear="all">

[Slim](https://github.com/yterajima/slim/blob/README_ja/README.md)は、こんな感じで記述していきます。

{% codeblock lang:html test.slim %}
{% raw %}
| ---
  layout: default
  ---

div.heading#toc
  h2 目次

div class="section toc"
  div.col
    h4
      a href="#character" 登場人物
    ul
      li
        a href="#character-yui" 月詠 唯(つくよみ ゆい)
      li
        a href="#character-sakura" 宮本 桜(みやもと さくら)
  div.col
    h4
      a href="#world" 世界観
    ul
      li
        a href="#world-city" 魔法都市
      li
        a href="#world-japan" 日本

div.section#golden-rule
  div.col
    h4 一人の少女が世界を変えた物語

  div.col
    blockquote この物語はフィクションです。

div.heading#character
  h2 登場人物

div.section#character-yui
  div.col
    h3 月詠 唯(つくよみ ゆい)
    ul
    p サボテンを持つ、黒髪の少女。いつも目を閉じている。見た目は7歳の女の子だが、年齢不詳
  div.col
    | {% highlight sh %}{% include txt/character-yui.txt %}{% endhighlight %}

div.heading#world
  h2 世界観

div.section#world-city
  div.col
    h3 魔法都市
    ul
    p 魔法都市は、有能な魔法使い7人によって創設され、人口の7割が17歳以下で占める近代急成長している一国。ただし、世界政府からは国として認められていない
  div.col
    | {% highlight sh %}{% include txt/world-city.txt %}{% endhighlight %}

div.section#world-japan
  div.col
    h3 日本
    p 現在、魔法都市がある地区だが、かつては日本と呼ばれていた。現在は大半の地域が壊滅している
  div.col
    | {% highlight sh %}{% include txt/world-japan.txt %}{% endhighlight %}

{% endraw %}
{% endcodeblock %}

そして、例えば、`$ slimrb -p test.slim test.html`コマンドを実行すると、以下のようになります。

{% codeblock lang:html test.html %}
{% raw %}
---
layout: default
---
<div class="heading" id="toc">
  <h2>
    目次
  </h2>
</div>
<div class="section toc">
  <div class="col">
    <h4>
      <a href="#character">登場人物</a>
    </h4>
    <ul>
      <li>
        <a href="#character-yui">月詠 唯(つくよみ ゆい)</a>
      </li>
      <li>
        <a href="#character-sakura">宮本 桜(みやもと さくら)</a>
      </li>
    </ul>
  </div>
  <div class="col">
    <h4>
      <a href="#world">世界観</a>
    </h4>
    <ul>
      <li>
        <a href="#world-city">魔法都市</a>
      </li>
      <li>
        <a href="#world-japan">日本</a>
      </li>
    </ul>
  </div>
</div>
<div class="section" id="golden-rule">
  <div class="col">
    <h4>
      一人の少女が世界を変えた物語
    </h4>
  </div>
  <div class="col">
    <blockquote>この物語はフィクションです。</blockquote>
  </div>
</div>
<div class="heading" id="character">
  <h2>
    登場人物
  </h2>
</div>
<div class="section" id="character-yui">
  <div class="col">
    <h3>
      月詠 唯(つくよみ ゆい)
    </h3>
    <ul></ul>
    <p>
      サボテンを持つ、黒髪の少女。いつも目を閉じている。見た目は7歳の女の子だが、年齢不詳
    </p>
  </div>
  <div class="col">
    {% highlight sh %}{% include txt/character-yui.txt %}{% endhighlight %}
  </div>
</div>
<div class="heading" id="world">
  <h2>
    世界観
  </h2>
</div>
<div class="section" id="world-city">
  <div class="col">
    <h3>
      魔法都市
    </h3>
    <ul></ul>
    <p>
      魔法都市は、有能な魔法使い7人によって創設され、人口の7割が17歳以下で占める近代急成長している一国。ただし、世界政府からは国として認められていない
    </p>
  </div>
  <div class="col">
    {% highlight sh %}{% include txt/world-city.txt %}{% endhighlight %}
  </div>
</div>
<div class="section" id="world-japan">
  <div class="col">
    <h3>
      日本
    </h3>
    <p>
      現在、魔法都市がある地区だが、かつては日本と呼ばれていた。現在は大半の地域が壊滅している
    </p>
  </div>
  <div class="col">
    {% highlight sh %}{% include txt/world-japan.txt %}{% endhighlight %}
  </div>
</div>
{% endraw %}
{% endcodeblock %}

適当な記事ですいません。ちょっと触ってみただけなので、よく分かっていません。以下のものが便利です。

<a href="https://github.com/slim-template/vim-slim" target="_blank">slim-template/vim-slim</a>

<a href="http://blogged.e2esound.com/2013/07/22/21_tips_to_use_slim_for_markup_engineer/" target="_blank">マークアッパー的 Slim 入門21の手引き | e2esound.com業務日誌</a>

