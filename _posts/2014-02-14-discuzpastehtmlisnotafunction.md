---
title: 140214 discuz pasteHTML is not a function
layout: post
permalink: /2741.html
categories:
  - Code
tags:
  - discuz
  - pasteHTML
  - x3
---
discuz发表文章的时候，editor.js触发关于表情插入点击会报错 pasteHTML is not a function，会在ie9,firefox中出现。 网上查了下x3 x3.1 都有类似问题不过在过去的补丁里面discuz已经修复了。 例如：http://www.discuz.net/thread-3480872-1-1.html 不过可能有一些公司是不会随着discuz版本而升级，有些BUG比较难查，类似这个。 修复方法： //修改 static/js/editor.js中 function insertText(text, movestart, moveend, select, sel) { checkFocus(); if(wysiwyg) { try { var sel = editdoc.getSelection(); if(!sel || sel.type.toString().toLowerCase() == 'none'){ editdoc.getElementsByTagName('body')[0].focus(); } var range = sel.getRangeAt(0); if(range && range.insertNode) { range.deleteContents(); } var frag = range.createContextualFragment(text); var lnode = frag.lastChild; range.insertNode(frag); range.setEndAfter(lnode); range.setStartAfter(lnode); sel.removeAllRanges(); sel.addRange(range); }... //修改为： function insertText(text, movestart, moveend, select, sel) { checkFocus(); if(wysiwyg) { try { var sel = editdoc.getSelection(); var range = sel.getRangeAt(0); if(range && range.insertNode) { range.deleteContents(); } var frag = range.createContextualFragment(text); var lnode = frag.lastChild; range.insertNode(frag); range.setEndAfter(lnode); range.setStartAfter(lnode); sel.removeAllRanges(); sel.addRange(range); }...