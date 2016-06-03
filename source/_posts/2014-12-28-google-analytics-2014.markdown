---
layout: post
title: "Google Analytics API"
date: 2014-12-28
comments: true
categories: [blog,programming]
tags: ruby
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">Google Analyticsを使って、アクセス数を調べてみた<!--more--><br clear="all">

[Google Console](https://code.google.com/apis/console/)を使って、APIを使えるようにしておき、JSONをダウンロードします。スクリプトディレクトリに`client_secrets.json`として保存します。


![](http://lh3.ggpht.com/-cS_i9Nfu5bs/VJ-vw6aQo-I/AAAAAAAAAM0/MrDsrCjqIiQ/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

![](http://lh3.ggpht.com/-txBeuq2Zmnw/VJ-vxVZePzI/AAAAAAAAAM4/BZK5yKKijZE/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)


![](http://lh4.ggpht.com/-8zVc2PQtiLc/VJ-vwS4bXEI/AAAAAAAAAMs/FydjN9B655c/%2525E3%252582%2525B9%2525E3%252582%2525AF%2525E3%252583%2525AA%2525E3%252583%2525BC%2525E3%252583%2525B3%2525E3%252582%2525B7%2525E3%252583%2525A7%2525E3%252583%252583%2525E3%252583%252588%2525201.png)

{% codeblock lang:bash %}
$ gem install google-api-client
{% endcodeblock %}


{% codeblock lang:ruby analytics.rb http://qiita.com/kazuph/items/2cf81a84985e894e9682 LINK %}
{% raw %}
#!/usr/bin/env ruby
# coding : utf-8

# 参考
# https://github.com/google/google-api-ruby-client
# https://github.com/google/google-api-ruby-client-samples/tree/master/adsense
# https://developers.google.com/api-client-library/ruby/guide/aaa_oauth
# http://blog.naberon.jp/post/2013/08/25/google-analytics-api/

# こっちのモジュールも良さそう
# http://tsuchikazu.net/googel_analytics_gar/

require 'pp'
require 'json'
require 'pry'
require 'google/api_client'
require 'google/api_client/client_secrets'
require 'google/api_client/auth/installed_app'
require 'google/api_client/auth/file_storage'

CREDENTIAL_STORE_FILE = "#{$0}-oauth2.json"

# Analytics profile ID.
# https://www.google.com/analytics/web/#home/a42353636w43552078pXXXXXXXX/
# なURLのpのあと数字がProfile ID
profileID = 'xxxxxxxxx'

client = Google::APIClient.new(
  :application_name => 'TestProject',
  :application_version => '0.0.1'
)

analytics = client.discovered_api('analytics', 'v3')

store = Google::APIClient::FileStore.new(CREDENTIAL_STORE_FILE)
  authfile = Google::APIClient::Storage.new(store)
  authfile.authorize
#authfile = Google::APIClient::FileStorage.new(CREDENTIAL_STORE_FILE)

unless authfile.authorization.nil?
  client.authorization = authfile.authorization
else
  # ここでDLしたJSONを読み込んでいるので同じディレクトリにclient_secrets.jsonを置いておくこと
  client_secrets = Google::APIClient::ClientSecrets.load

  flow = Google::APIClient::InstalledAppFlow.new(
    :client_id     => client_secrets.client_id,
    :client_secret => client_secrets.client_secret,
    :scope         => ['https://www.googleapis.com/auth/analytics.readonly']
  )

  client.authorization = flow.authorize
  #storage.write_credentials(client.authorization)
  authfile.write_credentials(client.authorization.dup) # 認証情報をファイルに保存
end

startDate = DateTime.now.prev_month.strftime("%Y-%m-%d")
endDate   = DateTime.now.strftime("%Y-%m-%d")

result = client.execute(
  :api_method => analytics.data.ga.get,
  :parameters => {
    'ids'        => "ga:" + profileID,
    'start-date' => startDate,
    'end-date'   => endDate,
    'metrics'    => 'ga:visitors,ga:visits,ga:pageviews',
    'dimensions' => 'ga:pagePath,ga:pageTitle',
    'sort'       => '-ga:pageviews'
  }
)

body = JSON.parse(result.response.body)
body['rows'].each do |row|
  pp row
end
{% endraw %}
{% endcodeblock %}

認証情報が保存されてない場合は、ブラウザを開き、保存します。ファイルは、`#{$0}-oauth2.json`です。

{% codeblock lang:bash %}
{% raw %}
$ ./analytics.rb| jq -r '.[1,3]' | head -n 20
{% endraw %}
{% endcodeblock %}

あまりアクセスはなく、アドベントカレンダーでしか人が来てないことが分かります。

{% raw %}
    MBA-HACK2
    449
    Vimのマークについて - MBA-HACK2
    580
    zshで使用頻度が高いもの - MBA-HACK2
    240
    Webサービスを整理してみた - MBA-HACK2
    72
    Bootstrapのメニューバーをマウスオーバーで開く - MBA-HACK2
    41
    Arch Linux GUI - MBA-HACK2
    12
    AIと会話をしてみたよ - MBA-HACK2
    13
    MBA-HACK2
    0
    システム情報の確認にinxiが便利だった件 - MBA-HACK2
    9
    Arch LinuxのChromiumが文字化けする - MBA-HACK2
    20
{% endraw %}

これで、人気記事順に表示するプラグインとか作れそうですね。
