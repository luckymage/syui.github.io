---
layout: post
title: "airgoogleplus"
date: 2014-06-15
comments: true
categories: [programming, tool]
tags: [mac, shell, google, terminal, tool, sns, api]
---


<img src="{{ root_url }}/images/more.png" width="100" height="100" alt="phoenix-power" align="left" >airgoogleplusのコードを解説します。<!--more--><br clear="all">


https://github.com/syui/airgoogleplus

##README.md

###features

This article explains the features in airgoogleplus.

airgoogleplus is a Google+ client running on the command line.

airgoogleplus is will only support Mac, And some functions only support of iTerm Terminal.

###japanese

この文書は、 airgoogleplus の機能について解説します。

airgoogleplus は、コマンドラインで動作する Google+ クライアントです。

airgoogleplus は、 Mac のみに対応しています。そして、一部機能は、端末の iTerm を使用します。

###install

####json download

まずは、プロジェクトを作り、 Google+ API を ON にしてください。

{% codeblock lang:bash %}
$ open -a Google\ Chrome https://console.developers.google.com/project
{% endcodeblock %}

そこで、 json ファイルをダウンロードします。

{% codeblock lang:bash %}
$ cp ~/Downloads/userID.json /path/to/airgoogleplus/txt
{% endcodeblock %}







####OAuth 2.0

認証を行います。[percol](https://github.com/mooz/percol)を導入している場合はメニューを使えます。

認証は、ブラウザの Google Chrome を通して行います。

{% codeblock lang:bash %}
$ git clone https://github.com/syui/airgoogleplus

$ cd !$:t

$ !$
{% endcodeblock %}

メニューなしでも以下のコマンドで OAuth 2.0 認証ができます。

{% codeblock lang:bash %}
$ git clone https://github.com/syui/airgoogleplus

$ cd !$:t

$ !$ air-o
{% endcodeblock %}


###Google+ API

[Google+ API Help](https://developers.google.com/+/api/?hl=ja)

> Google+ API は Google+ に対するプログラミング インターフェースです。API を使用してアプリまたはウェブサイトを Google+ と統合できます。ユーザーは、アプリケーション内から Google+ の機能を使用して、互いにつながり、最大限のエンゲージメントを得られます。

####people get me

名前、写真画像、プロフィール URL など、プロフィールを構成する自分の情報を取得します。

{% codeblock lang:bash %}
$ airgoogleplus air-j
{% endcodeblock %}

####activity get userID

ユーザーのアクティビティ、投稿情報を取得します。これには、userIDとactivityIDが必要になります。

IDの取得は、メニューを使って行います。

{% codeblock lang:bash %}
$ airgoogleplus air-m

<C-u>get acti<CR>
{% endcodeblock %}





###directory

私が作るツールのディレクトリ構造を解説します。

{% codeblock lang:bash %}
.
├── LICENSE #ライセンス:cc0
│
├── README.md #説明書
│
├── airgoogleplus #本体:ディレクトリ名
│
├── tool #外部ツール、ダウンロードファイル
│
├── script #スクリプト、実行ファイル
│   │  
│   ├── menu.sh
│   │  
│   └── huga.sh
│
├── backup #txtフォルダのバックアップです
│   │  
│   └── theme.txt
│ 
├── t #テスト
│   │  
│   └── test.sh
│ 
└── txt #テキスト、テーマファイルなど
    │  
    └── theme.txt
{% endcodeblock %}

本体にテーマファイル`/txt/theme.txt`を読み込ませ、テーマごとに処理を書いていきます。スクリプトが多くなる場合は、`/script/menu.sh`を作り、更に処理を分けます。

個人情報は、`/txt`に保存されます。

個人情報を扱う場合は、`script/delete.sh`にて、一括削除を実行できるようにします。

この際、個別に削除するのではなく、`/txt`を一括削除します。

したがって、`/txt`の初期設定は、`/backup`に保存してあります。削除後は、バックアップからリカバリされます。

###code

`airgoogleplus`のコードを解説します。

####airgoogleplus

本体ファイルです。基本的には、テーマファイルを読み取り、スクリプトの実行を行います。スクリプトの実行は、`/path/to/airgoogleplus/script/menu.sh`を介して実行される場合があります。

{% codeblock lang:bash /path/to/airgoogleplus/airgoogleplus %}
#!/bin/zsh

# パスの取得
dir=${0:a:h}
scpt=$dir/script
them=$dir/txt/theme.txt

# 引数がない場合とある場合の処理
if (( ${#*} == 1 )); then
    opt=$1
else
    # 引数がない場合は、テーマファイルを percol で表示する
    opt=`cat $them | percol --query="air-" | cut -d ":" -f 1`
fi

# percol がない場合は、`path/to/tool`にダウンロードし、インストールする
$scpt/download_tool_percol.sh

case $opt in

    "air-o")
        $scpt/googleapi_access_token.sh
        ;;

    *)
        exit
        ;;
esac

exit 0
{% endcodeblock %}

####menu.sh

重要なスクリプトは、1つの単純な単語により構成するようにしている。例えば、`menu.sh`など。

反対に、基本的なスクリプトは、3つの単語により構成する。例えば、`chrome_open_url.sh`など。単語の区切りは、アンダーバー`_`を使用することが多い。

{% codeblock lang:bash /script/menu.sh %}
{% raw %}
#!/bin/zsh

# 指定のファイル、ディレクトリの有無を調べる
if [ -e $acce ]; then

    # 認証に必要な情報を取得(アクセストークン)
    access=`cat $txt/access.txt | jq -r .access_token` > /dev/null 2>&1

    # APIを使用するためのトップアドレスを取得し、それを percol で検索指定する
    url=`cat $http | percol --query="https://www.googleapis.com/"`

    # URLに`userId`が含まれる場合の処理
    if echo $url | grep "{userId}" > /dev/null 2>&1; then
        echo -n "userId: "
        # 端末からの入力待ち
        read key
        # アドレスを`sed`に対応する
        url=`echo $url | sed 's/\//\\//g'`
        # 入力した`userId`をアドレスに変換する
        url=`echo $url | sed "s/{userId}/$key/g"`
    fi

    # URLに`get_userId`が含まれる場合の処理
    if echo $url | grep "{get_userId}" > /dev/null 2>&1; then
        # フォロー中のユーザー情報が取得出来ているか
        if [ -e $foll ];then
                # `userId`を取得するスクリプトの実行
                key=`$scpt/googleplus_id_user.sh`
                url=`cat $http | percol --query="userId"`
                url=`echo $url | sed 's/\//\\//g'`
                url=`echo $url | sed "s/{userId}/$key/g"`
        else
                $scpt/googleplus_get_follow.sh > /dev/null 2>&1
                # フォロー中のユーザー情報を取得するスクリプトの実行
                key=`$scpt/googleplus_id_user.sh`
                url=`cat $http | percol --query="userId"`
                url=`echo $url | sed 's/\//\\//g'`
                url=`echo $url | sed "s/{userId}/$key/g"`
        fi
    fi

# Google+ API HTTP
curl -H "Authorization: Bearer $access" $url

else
    echo no...access token
fi

exit 0
{% endraw %}
{% endcodeblock %}

####googleapi_access_token.sh

{% codeblock lang:bash googleapi_access_token.sh %}
{% raw %}
#!/bin/zsh

if [ `cat $txt/access.txt | jq -r .access_token` != null ] ; then

    # リフレッシュトークンの処理
    $scpt/googleapi_refresh_token.sh

else

    $scpt/download_json_googleapi.sh

    if ls $txt/*.json > /dev/null 2>&1; then

        # .jsonで書かれたファイルから`jq`を使って、必要なデータを取得
        id=`cat $txt/*.json | jq -r .web.client_id`
        sec=`cat $txt/*.json | jq -r .web.client_secret`
        url=`cat $txt/*.json | jq -r .web.redirect_uris`

        # Google Chromeを使って OAuth2認証 を行う
        open -a Google\ Chrome "https://accounts.google.com/o/oauth2/auth?client_id=$id&redirect_uri=http%3A%2F%2Flocalhost%2Foauth2callback&scope=https://www.googleapis.com/auth/plus.circles.read%20https://www.googleapis.com/auth/plus.login%20https://www.googleapis.com/auth/plus.me%20https://www.googleapis.com/auth/userinfo.email&response_type=code&access_type=offline&approval_prompt=force"
        #&approval_prompt=forcee

        # ブラウザのリロード完了を待ち、ターミナルに戻る
        $scpt/chrome_done_reload.sh && $scpt/iterm_activate_window.sh

        # Enterを押して、次の処理へ
        echo enter
        read key

        # アクセストークンの取得に必要な情報をURLから得る
        url=`$scpt/chrome_get_url.sh`
        code=`echo $url | cut -d '=' -f 2`
        rm $txt/code.txt > /dev/null 2>&1
        echo $code > $txt/code.txt

        rm $txt/access.txt > /dev/null 2>&1

        # アクセストークンの発行と保存
        curl -d client_id=$id -d client_secret=$sec -d redirect_uri=http%3A%2F%2Flocalhost%2Foauth2callback -d grant_type=authorization_code -d code=$code https://accounts.google.com/o/oauth2/token > $txt/access.txt

        cat $txt/access.txt

        # アクセストークンの確認
        access=`cat $txt/access.txt | jq -r .access_token`

        # Google+ APIを使って自分の情報を取得
        curl -s "https://www.googleapis.com/oauth2/v1/tokeninfo?access_token=$access"

    else

        echo no...json

    fi

fi

exit 0
{% endraw %}
{% endcodeblock %}

####googleapi_next_pagetoken.sh

Google API は、情報が多い場合、情報の取得数を制限している。

したがって、全部の情報の取得には、`next_pagetoken`の処理が必要になります。

これは、最初や最後ではなく、処理中に記述しなければならない場合が多いので、スクリプトとして実行する場面が少ない。

{% codeblock lang:bash googleapi_next_pagetoken.sh %}
{% raw %}
#!/bin/zsh

# nextPageToken {{{
ptoken=`curl -s -H "Authorization: Bearer $access" $url | jq -r .nextPageToken` > /dev/null 2>&1
until [ "$ptoken" = "null" ]
do
   url=https://www.googleapis.com/plus/v1/people/me/people/visible?pageToken=$ptoken
   curl -s -H "Authorization: Bearer $access" $url
   ptoken=`curl -s -H "Authorization: Bearer $access" $url | jq -r .nextPageToken` > /dev/null 2>&1
done
# nextPageToken }}}

exit 0
{% endraw %}
{% endcodeblock %}

####googleapi_refresh_token.sh

Google API の`OAuth2.0`認証は、期限付きの場合が多く、数分でアクセストークンが切れてしまう。

そのため、継続して使用するためにリフレッシュトークンの取得と活用が必要になってくる。

リフレッシュトークンを取得するには、アクセストークンの取得時に、`access_type=offline`と`approval_prompt=force`が必要みたいです。この辺りは、非常に曖昧で複雑。

このスクリプトは、他のすべてのスクリプトで実行しなければならないので、辛い。

{% codeblock lang:bash googleapi_refresh_token.sh %}
{% raw %}
#!/bin/zsh

if [ -e $txt/access.txt ]; then

access=`cat $txt/access.txt | jq -r .access_token`

# アクセストークンが有効な時間を見て、既に切れていた場合、リフレッシュトークンを使う
if [ `$scpt/googleapi_token_time.sh` = "null" ]; then
    id=`cat $txt/*.json | jq -r .web.client_id`
    sec=`cat $txt/*.json | jq -r .web.client_secret`
    code=`cat $txt/access.txt | jq -r .refresh_token`
    rm $txt/access.txt > /dev/null 2>&1
    curl -d client_id=$id -d client_secret=$sec -d refresh_token=$code -d grant_type=refresh_token https://accounts.google.com/o/oauth2/token > $txt/access.txt
    access=`cat $txt/access.txt | jq -r .access_token`
    curl -s "https://www.googleapis.com/oauth2/v1/tokeninfo?access_token=$access"
fi

else
    echo no...json
fi

exit 0
{% endraw %}
{% endcodeblock %}

####unfollow.sh

相互フォローを支援するスクリプト。

フォロー中のユーザー情報は API で取得できるもののフォローされいてるユーザーは、ブラウザを使ってでしか取得できない。

したがって、少し複雑になるが、要は、フォロー、フォロワーのIDの齟齬を抽出し、それをブラウザで表示するというもの。

{% codeblock lang:bash unfollow.sh %}
{% raw %}
#!/bin/zsh

# Google+ APIを使い、フォローの`userId`を取得する
$scpt/googleplus_get_follow.sh

# ブラウザを開き、ソースを保存する
$scpt/chrome_copy_haveyou.sh

$scpt/googleplus_get_haveyou.sh

$scpt/googleplus_get_unfollow.sh

echo -e "[y]es | [n]o : "
read key

case $key in
    y|[yY]es)
        $scpt/chrome_open_unfollow.sh;;
    n|[nN]o)
        echo no...open browser;;
    *)
        echo no...open browser;;
esac

exit 0
{% endraw %}
{% endcodeblock %}

####googleplus_get_haveyou.sh

フォロワーの`userId`を取得する。

{% codeblock lang:bash googleplus_get_haveyou.sh %}
{% raw %}
#!/bin/zsh

if [ -e $have ]; then
        rm $foid > /dev/null 2>&1
        cat $have |  grep -e "ppv.psn" | head -n 1 | cut  -d '"' -f 6 > $foid
        cat $have | grep -e "ppv.psn" | sed '1d' | cut -d '"' -f 4 | grep -v -e "ppv.psn" >> $foid
        cat $foll | jq -r '.items[].id' >> $foid
fi

exit 0
{% endraw %}
{% endcodeblock %}

####googleplus_get_unfollow.sh

{% codeblock lang:bash googleplus_get_unfollow.sh %}
{% raw %}
#!/bin/zsh

rm $unli > /dev/null 2>&1
# 並び替えと2つのファイルの違いを抽出
sort $foid | uniq -u > $unli
cat $unli

exit 0
{% endraw %}
{% endcodeblock %}

