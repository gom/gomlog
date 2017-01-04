---
title: Wordpress2.5へのアップデートとfaviconの設置
date: 2008-04-02
tags: [ wordpress ]
url: 20080402_wordpress-update
hidden: true
---
WordPress2.5にアップデートした。

<h4>いつのまにか変わってた</h4>
以前はUTF-8対応のため、/wp-includes/wp-db.phpの89行目付近に1行追加していた。
WordPress2.2以上では、上記ファイルに手を加える必要がなくなったらしい。
全く気づいてなかった･･･
代わりにwp-config.phpに以下の設定が追加されていた。

<blockquote>
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', '');
</blockquote>

デフォルト値がUTF-８なので、これでOK。楽になったもんだ。

参考：<a href="http://bono.s201.xrea.com/2006/05/12-utf8_xrea_4/">power source* » XREAにUTF8設置時の文字化け： 4）設置方法まとめ</a>
<a href="http://gomlog.com/20070127_wordpress_euc_to_utf8/">Wordpress::EUCからUTF8への移行方法 : gomlog</a>

<h4>ついでにfavicon</h4>
勢いでfaviconも作ってしまった。ブラウザの端っこの方に小さく表示されている･･･はず！
イラレが3回吹き飛んだのでどんどん手抜きになっていったけど、元から手抜きなんで気にしない。
