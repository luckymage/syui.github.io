---
layout: post
title: "jekyll-toc-generatorを個別ページで表示する場合の問題点"
date: 2014-07-07
comments: true
categories: [blog]
tags: [octopress, github, jekyll]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">インデントの再形成が悪影響を及ぼすようです。<!--more--><br clear="all">


##はじめに

<a href="http://syui.github.io/blog/2014/07/06/github-toc-plugin/" target="_blank">jekyll-toc-generator</a>で目次を作成する方法を紹介しました。

しかし、いくつかの問題がありますので、それを説明します。

##問題点

###現在確認している問題点

- 個別ページで表示する場合に、[Codeblock](http://octopress.org/docs/plugins/codeblock/)の表示が一部おかしくなります。

- 上記問題は、インデントが形成されてしまうことによる問題です。

- インデントの形成は、どうやら`figcaption`(タイトル)を付けていない場合に発生するようです。

###個別ページへの目次の表示

私の場合は、以下のファイルを編集することで、個別ページに目次を表示することができます。

{% raw %}
    {{ content | toc_generate }}
{% endraw %}

{% codeblock lang:html ~/octopress/source/_includes/article.html %}
{% raw %}
<div class="entry-content clearfix">
    {{ content | toc_generate }}
</div>
{% endraw %}
{% endcodeblock %}

###インデントの形成

しかし、これでプレビューすると、コード部分が以下の様なソースに変化してしまします。これにより表示崩れが起こります。

####プラグイン導入前

{% codeblock lang:html %}
{% raw %}
<figure class="code"><div class="highlight"><table><tbody><tr><td class="gutter"><pre class="line-numbers"><span class="line-number">1</span>
</pre></td><td class="code"><pre><code class="bash"><span class="line"><span class="nv">$ </span>osascript -e <span class="s1">'tell application "iTerm" to activate'</span>
</span></code></pre></td></tr></tbody></table></div></figure>
{% endraw %}
{% endcodeblock %}

####プラグイン導入後

{% codeblock lang:html %}
{% raw %}
<figure class="code">
   <div class="highlight">
      <table>
         <tbody><tr>
            <td class="gutter">
               <pre class="line-numbers"><span class="line-number">1</span>
</pre>
            </td>
            <td class="code">
               <pre>                  <code class="bash">
                     <span class="line"><span class="nv">$ </span>osascript -e <span class="s1">'tell application "iTerm" to activate'</span>
</span>
                  </code>
               </pre>
            </td>
         </tr>
      </tbody></table>
   </div>
</figure>
{% endraw %}
{% endcodeblock %}

コードの内容は同じなのですが、インデントが形成されることによって、表示が崩れてしまいます。

###問題の原因と解決法

- 問題の原因は、プラグイン本体の以下のコード辺りにあります。

> <a href="https://github.com/dafi/jekyll-toc-generator/blob/master/_plugins/tocGenerator.rb#L95" target="_blank">https://github.com/dafi/jekyll-toc-generator/blob/master/_plugins/tocGenerator.rb#L95</a>

- この問題の解決法は、Markdownが変換されるタイミングを調整するか、本体のコードを書き換えることが考えられます。

{% codeblock lang:ruby tocGenerator.rb https://github.com/dafi/jekyll-toc-generator/blob/master/_plugins/tocGenerator.rb#L95 LINK %}

- doc.css('body').children.to_xhtml(indent:3, indent_text:" ")

+ doc.css('body').children.to_html
{% endcodeblock %}

