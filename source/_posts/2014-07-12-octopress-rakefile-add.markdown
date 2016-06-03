---
layout: post
title: "「rake new_post」する場合の書式を変更する"
date: 2014-07-12
comments: true
categories: [blog]
tags: [octopress]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Rakefileを書き換えます。<!--more--><br clear="all">

常に`<!--more-->`を使うので、変更してみました。

{% codeblock lang:ruby Rakefile %}
{% raw %}
  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
    post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M:%S %z')}"
    post.puts "comments: true"
    post.puts "categories: "
    post.puts "tags: "
    post.puts "---"

    post.puts '<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100"><!--more--><br clear="all">'
  end
{% endraw %}
{% endcodeblock %}
