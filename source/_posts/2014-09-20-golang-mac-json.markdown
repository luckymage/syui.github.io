---
layout: post
title: "GoでJSONデータを扱う方法"
date: 2014-09-20
comments: true
categories: [ os, programming]
tags: [ golang, mac, json]
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">golangを触ってみました。<!--more--><br clear="all">


##golang

###gojson

https://github.com/ChimeraCoder/gojson

{% codeblock lang:bash %}
$ sudo go get github.com/ChimeraCoder/gojson
{% endcodeblock %}

ここで、なぜかエラーが出ます。よくわからないのですが、ビルドが実行されてない感じなので、手動ビルドすることにしました。

{% codeblock lang:bash %}
$ cd $GOPATH/src/!$

$ sudo go build json-to-struct.go

$ curl -s https://api.github.com/repos/chimeracoder/gojson | ./json-to-struct -name=Repository
{% endcodeblock %}

###web server

通常は、こんな感じで、ディレクトリ管理するのですが、今回はやりません。

{% codeblock lang:bash %}
$ mkdir -p $GOPATH/src/github.com/user/webserver

$ cd !$

$ sudo go install
{% endcodeblock %}

Web Serverを立ち上げてみます。そこに、JSONデータを置くことにしましょう。

{% codeblock lang:go main.go http://www.alexedwards.net/blog/golang-response-snippets LINK %}
package main

import (
  "encoding/json"
  "net/http"
)

type Profile struct {
  Name    string
  Hobbies []string
}

func main() {
  http.HandleFunc("/", foo)
  http.ListenAndServe(":3000", nil)
}

func foo(w http.ResponseWriter, r *http.Request) {
  profile := Profile{"syui", []string{"snowboarding", "programming"}}

  js, err := json.Marshal(profile)
  if err != nil {
    http.Error(w, err.Error(), http.StatusInternalServerError)
    return
  }

  w.Header().Set("Content-Type", "application/json")
  w.Write(js)
}
{% endcodeblock %}

サーバーを立ち上げると、以下のリクエストを返します。

{% codeblock lang:bash %}
$ sudo go run main.go

$ curl -i localhost:3000
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 56
{"Name":"syui",Hobbies":["snowboarding","programming"]}
{% endcodeblock %}

`gojson`を使ってみると、こんな感じです。`./json-to-struct`

{% codeblock lang:bash %}
{% raw %}
$ curl -s localhost:3000 | gojson

package main

type Foo struct {
  Hobbies []string `json:"Hobbies"`
  Name    string   `json:"Name"`
}
{% endraw %}
{% endcodeblock %}

###http log

ログとかも表示したりできますので、応用可能性が広がります。

http://qiita.com/futoase/items/ea86b750bbb36d7d859a

