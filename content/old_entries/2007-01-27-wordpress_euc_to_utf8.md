---
title: Wordpress--EUCからUTF8への移行方法
date: 2007-01-27
tags: [ blog, diary, wordpress ]
url: 20070127_wordpress_euc_to_utf8
hidden: true
---
WordpressとMySQLの文字コードの不整合が起こっていたのですが、ようやく復旧しました。
ひっそりとサーバー移転。MｙSQL4→5になり、文字コードもUTF-8にしました。

管理画面へのアクセスに異常に時間がかかっていたのですが・・・これも解決しました。
快適です。

移行後の環境は
Web：Apache1.3.37
PHP5.1.6
MySQL5.1.11

以下、解決方法の紹介です。ちょっと長いですが、ご容赦ください。

<!--more-->
<div></div>
<div></div>
<div></div>
<div><strong>1.現象</strong>
まず、最初のサーバーでの設定。
Wordpress：EUC-JP
MySQL：EUC-JP</div>
<div>MySQLはEUC-JPを指定して作成したのですが、なぜか照合順序がUTF-８に。
初アクセス時にページが表示されない、管理画面に一回では繋がらない等の不具合が出てました。
<a href="http://www.technorati.jp/">Technorati (テクノラティ) </a>の表示リンクも文字化け状態。

そこで、文字コードを揃えて設定しなおすことにしました。</div>
<strong>2.データ移行</strong>
今度はUTF-8にしようと思い、サーバーアカウント取得。
Wordpress：UTF-8
MySQL：UTF-8
で設定し、旧サーバーでMySQLのバックアップを行う。

旧MySQL→新MySQLへデータを移行。
phpMyAdminのエクスポートとインポートを利用してます。
そのままエクスポート→インポートを行うと、文字コードがEUC-JPのままになり、MySQL内で文字化けが発生。
エクスポートされたSQL文をちょいと修正
<code>DEFAULT CHARSET=utf8</code>
おし、無事インポートできました。

<strong>3.文字化け対応</strong>
表示してみると･･･やはり文字化けが発生。
<a href="http://bono.s201.xrea.com/2006/05/12-utf8_xrea_4/">power source* » XREAにUTF8設置時の文字化け： 4）設置方法まとめ</a>
を参考にして修正。うまく表示されました。

<strong>4.権限のエラー解消</strong>
さて、設定を変えよう・・・あれ？管理画面に入れない？
ログインすると、下記のエラーが画面上部に表示される。

<code>
Warning: Invalid argument supplied for foreach() in (サーバーのディレクトリ)/wp-includes/capabilities.php on line 19
</code>

かろうじて管理画面のTOPが表示される。上記エラーはやっぱり表示されてる。
管理画面以下の投稿・設定画面にアクセスしようとすると・・・

<code>
Warning: Invalid argument supplied for foreach() in (サーバーのディレクトリ)/wp-includes/capabilities.php on line 19
あなたはこのページにアクセスする権限を持っていません。
</code>

capabilities.phpの19行目に一体何があるんだ！と思いつつ、フォーラムで同じ問題を発見。
<a href="http://phpbb.xwd.jp/viewtopic.php?p=2628">WordPress Japan :: トピックを表示 - WPをインストールしてログインすると権限エラーになってしまいま</a>

返信にこうあったのが大ヒントになりました。
<blockquote>新規インストール時に文字コードをUTF-8でインストールすると
日本語の権限表記にバックスラッシュが付与されてしまうようです。
**_option テーブルの **_user_roles の値を編集していただければ解決すると思います。</blockquote>
早速user_rolesを見てみたら・・・あった！
日本語権限名が全部文字化けしてる！

同様に提示されていた、
<a href="http://wordpress.xwd.jp/files/utf_patch.zip">http://wordpress.xwd.jp/files/utf_patch.zip</a>
を使用したところ、うまく修正されました。

<strong>6.終わりに</strong>
無事管理画面も使えるようになり、こうして投稿できたわけです・・・
最近は日本語の資料もだいぶ増えてきたので、そこそこスムーズに解決できました。
