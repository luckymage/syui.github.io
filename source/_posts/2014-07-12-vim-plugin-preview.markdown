---
layout: post
title: "airpreview.vim"
date: 2014-07-12
comments: true
categories: [programming, browser]
tags: [vim, github, chrome, applescript, shellscript]
---

<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">以前削除していたプラグインが必要になりましたので、再度書きました。<!--more--><br clear="all">

##はじめに

###リポジトリと依存

{% githubrepo syui/airpreview.vim %}

いつもの同じように`Google Chrome`対応です。

- Mac
- Google Chrome
- vim-submode

###特徴

仕組みは簡単で、オートロードモード`\ + sj`と通常モード`\ + j`を搭載しており、Vimの移動とChromeのスクロールが連動します。

テキストが保存された場合にリロードするキーを用意しました。

<a href="http://qiita.com/syui/items/152e5ba8e0ff722fa47f" target="_blank">VimでのMarkdownプレビューを快適にする方法を考えてみた - Qiita</a>

##インストール

{% codeblock lang:bash ~/.vimrc %}
NeoBundle 'syui/airpreview.vim'
{% endcodeblock %}

`$ vim +NeoBundleInstall`

##コード

###ソースとコメント

{% codeblock lang:vim airpreview.vim/plugin/airpreview.vim %}
{% raw %}
" スクリプトがあるディレクトリ
let s:air_current = expand("<sfile>:p:h")

" スクリプト上のディレクトリ
let s:air_dir_home= expand("<sfile>:p:h:h")
let s:air_dir_tool= expand("<sfile>:p:h:h") . "/tool"

" それぞれのシェルスクリプトへのパス
let s:air_file_reload = s:air_dir_tool . "/reload_chrome.sh"
"let s:air_file_reload = s:air_dir_tool . "/reload_watch.sh"
let s:air_file_scroll= s:air_dir_tool . "/scroll_chrome.sh"
let s:air_file_make= s:air_dir_tool . "/make_tmp.sh"

"com! -nargs=1 AirSilent
"\ | exe ':silent '.<q-args>
"\ | exe ':redr'

" テスト
" com! -nargs=0 -bar AirPreviewTest exe "!echo " . s:air_file_scroll

" Google Chrome、引数の数字でポートを開く
com! -nargs=1 -bar AirPreviewOpen
      \ | silent! exe "!open -a 'Google\ Chrome' http://localhost:<args>/"
      \ | redr!

" アドレスを保存
com! -nargs=1 -bar AirPreviewOpenSave
      \ | silent! exe "!" . s:air_dir_tool . "/make_tmp.sh http://localhost:<args>/"
      \ | redr!

" 保存したアドレスを開く
com! -nargs=0 -bar AirPreviewOpenAuto
      \ | silent! exe "!cat " s:air_dir_home . "/theme/url.txt | xargs -J % open -a 'Google Chrome' %"
      \ | redr!

" Google Chromeをリロード
com! -nargs=0 -bar AirPreviewReload
      \ | silent! exe "!" . s:air_file_reload . " &"
      \ | redr!

" watchの場合、停止
com! -nargs=0 -bar AirPreviewReloadStop
      \ | silent! exe "!pkill watch"
      \ | redr!

" スクロール下
com! -nargs=0 -bar AirPreviewScrolldown
      \ | exe "!" . s:air_file_scroll . " next 200 &"

" スクロール上
com! -nargs=0 -bar AirPreviewScrollup
      \ | exe "!" . s:air_file_scroll . " prev 200 &"

" マッピングを汚さない
nn <Plug>(AirPreviewOpen) :AirPreviewOpen<CR>
nn <Plug>(AirPreviewOpenAuto) :AirPreviewOpenAuto<CR>
nn <Plug>(AirPreviewOpenSave) :AirPreviewOpenSave<CR>
nn <Plug>(AirPreviewReload) :AirPreviewReload<CR>
nn <Plug>(AirPreviewReloadStop) :AirPreviewReloadStop<CR>
nn <Plug>(AirPreviewScrolldown) :AirPreviewScrolldown<CR>
nn <Plug>(AirPreviewScrollup) :AirPreviewScrollup<CR>

" vim-submodeの設定
call submode#enter_with('airpreview', 'n', '', '<Leader>j', ':AirPreviewScrolldown<CR>')
call submode#enter_with('airpreview', 'n', '', '<Leader>k', ':AirPreviewScrollup<CR>')
call submode#leave_with('airpreview', 'n', '', 'n')
call submode#map('airpreview', 'n', '', 'j', ':AirPreviewScrolldown<CR>')
call submode#map('airpreview', 'n', '', 'k', ':AirPreviewScrollup<CR>')

" カーソル移動するとスクロール下
fu! s:airpreview_autoscroll_down()
  aug airpreview_vimrc_down
    au!
      silent! au! airpreview_vimrc_up
      au CursorMoved * silent AirPreviewScrolldown
  aug END
endf

" カーソル移動するとスクロール上
fu! s:airpreview_autoscroll_up()
  aug airpreview_vimrc_up
    au!
      silent! au! airpreview_vimrc_down
      au CursorMoved * silent AirPreviewScrollup
  aug END
endf

" テキストが変更されたらGoogle Chromeをリロード
fu! s:airpreview_autoscroll_reload()
  aug airpreview_vimrc_reload
    au!
      au TextChanged * silent AirPreviewReload
  aug END
endf

" 設定したautocmdをすべて停止
fu! s:airpreview_autoscroll_stop()
  silent! au! airpreview_vimrc_down
  silent! au! airpreview_vimrc_up
  silent! au! airpreview_vimrc_reload
endf

" autocmdのキーマップ定義
nn <Plug>(AirPreviewAutoScrollDown) :call <SID>airpreview_autoscroll_down()<CR>
nn <Plug>(AirPreviewAutoScrollUp) :call <SID>airpreview_autoscroll_up()<CR>
nn <Plug>(AirPreviewAutoScrollReload) :call <SID>airpreview_autoscroll_reload()<CR>
nn <Plug>(AirPreviewAutoScrollStop) :call <SID>airpreview_autoscroll_stop()<CR>

"" setting
"nm <silent> <Leader>o <Plug>(AirPreviewOpen)
"nm <silent> <Leader>o <Plug>(AirPreviewOpenAuto)
"nm <silent> <Leader>r <Plug>(AirPreviewReload)
"nm <silent> <Leader>rr <Plug>(AirPreviewReloadStop)
"nm <silent> <Leader>j <Plug>(AirPreviewScrolldown)
"nm <silent> <Leader>k <Plug>(AirPreviewScrollup)

"nm <silent> <Leader>sj <Plug>(AirPreviewAutoScrollDown)
"nm <silent> <Leader>sk <Plug>(AirPreviewAutoScrollUp)
"nm <silent> <Leader>sr <Plug>(AirPreviewAutoScrollReload)
"nm <silent> <Leader>ss <Plug>(AirPreviewAutoScrollStop)
{% endraw %}
{% endcodeblock %}

