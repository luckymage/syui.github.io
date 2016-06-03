---
layout: post
title: "XMLからJSONに変換するスクリプト"
date: 2014-09-27
comments: true
categories: programming
tags: node
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">検索すると、最初に`node.js`のモジュールが出てきましたので、書いてみました。<!--more--><br clear="all">

https://github.com/buglabs/node-xml2json

{% codeblock lang:bash %}
$ npm install xml2json
{% endcodeblock %}


{% codeblock lang:js xml-json.js %}
{% raw %}
#!/usr/bin/env node
var parser = require('xml2json');
//var argv = require('node-argv')

var re = /(?:\.([^.]+))?$/;
var typ = process.argv[2]
var ext = re.exec(typ)[1];

if (ext === "xml") {
  var fs = require('fs')
    , filename = process.argv[2];
  fs.readFile(filename, 'utf8', function(err, xml) {
    if (err) throw err;
    console.log(xml)

    var json = parser.toJson(xml); //returns a string containing the JSON structure by default
  console.log(json);
  });

} else {
  var xml = process.argv[2];
  var json = parser.toJson(xml); //returns a string containing the JSON structure by default
  console.log(json);
}
{% endraw %}
{% endcodeblock %}

例えば、以下の様な内容のファイルがあるとします。

{% codeblock lang:bash %}
{% raw %}
$ cat test2.xml
<config><test>Hello</test><data>SomeData</data></config>
{% endraw %}
{% endcodeblock %}

この場合、以下のコマンドで`XML`から`JSON`に変換できます。

{% codeblock lang:bash %}
$ ./xml-json.js test2.xml

$ cat test2.xml | xargs ./xml-json.js
{% endcodeblock %}

<a href="http://popkirby.github.io/contents/nodeguide/style.html" target="_blank">Felix's Node.js Style Guide(和訳)</a>


