---
title: Wordpress -- Wordpress2.5.1以降でブックマークレットを使って投稿する
date: 2008-08-02
tags: [ wordpress ]
url: 20080802_wordpress_bookmarkret
hidden: true
---
Wordpress2.3までに使えていた投稿用ブックマークレットを使う方法。

以下のブックマークレットをブックマークに登録します。
自分のブログのURLに書き換えましょう。
<code>
javascript:if(navigator.userAgent.indexOf('Safari')>=%200){Q=getSelection();}else{Q=document.selection?
document.selection.createRange().text:document.getSelection();}
location.href='http://example.com/wp-admin/post-new.php?text='+encodeURIComponent(Q)+'&popupurl='+encodeURIComponent(location.href)+'&popuptitle='+encodeURIComponent(document.title);
</code>

投稿したいページでブックマークレットを押すと、投稿ページに飛びます。
本文に投稿したいページのURLが挿入されていれば成功。
