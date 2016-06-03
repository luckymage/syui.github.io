---
layout: post
title: "Octopressにカテゴリとタグを分けて表示する"
date: 2014-06-22
comments: true
categories: [blog]
tags: [octopress, tag, plugin]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Octopress には、最初から Tag Clound というプラグインが入っていますが、その実態は、 Category Cloud なので、変更します。<!--more--><br clear="all">

まず、下記の記事の通りにやれば問題無いです。

<a href="http://akira-hamada.github.io/blog/2013/04/28/add_tag_cloud/" target="_blank">octopressにタグクラウドを追加する - the Code is in the Details</a>

すごく面倒ですよね。私はエディタで編集しましたが、スクリプトを作ったほうが簡単かもしれません。

{% codeblock lang:bash %}
#!/bin/bash
dir1=$1
dir2=$2
dir3=$3

co1="sed -i '' -e 's/Category/Tag/g'"
co2="sed -i '' -e 's/Categories/Tags/g'"
co3="sed -i '' -e 's/category/tag/g'"
co4="sed -i '' -e 's/categories/tags/g'"
co5="sed -i '' -e 's/category_dir/tag_dir/g'"

co1 $1
co1 $2
co1 $3
{% endcodeblock %}

{% codeblock lang:css %}
#27行目
-a.category, time {
+a.category, a.tag, time {

#63行目
-a.category {
+a.category, a.tags {

#68行目
-#content > .category {
+#content > .category, .tag {
{% endcodeblock %}

{% codeblock lang:html source/_includes/custom/asides/tag_cloud.html %}
{% raw %}
<section class="panel panel-default">
  <div class="panel-heading">
    <div class="panel-title">Tag Cloud</div>
  </div>

    <div class="panel-tag-cloud">
    <span id="tag-cloud">{% tag_cloud counter:true %}</span>
    </div>
</section>
{% endraw %}
{% endcodeblock %}

ちょっと間が開いてたほうが良かったので調整。

{% codeblock lang:css %}
div.panel-tag-cloud {
  padding: 10px 15px;
}
{% endcodeblock %}



書式は`tags: [hoge, huga]`というようにしてやればよいです。

      layout: post
      title: "Octopressにカテゴリとタグを分けて表示する"
      date: 2014-06-22
      comments: true
      categories: [blog]
      tags: [octopress, tag, plugin]
