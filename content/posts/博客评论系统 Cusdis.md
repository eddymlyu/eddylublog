---
title: "博客评论系统 Cusdis"
date: 2026-03-24T09:10:56+08:00
draft: false
url: "posts/cusdis"

tags: []
categories: ["tech"]
---

Hugo 里加一段 HTML，在你的文章模板里（通常是）：
```
layouts/_default/single.html
```


在文章底部加：
```
<div id="cusdis_thread"
  data-host="https://cusdis.com"
  data-app-id="你的APP_ID"
  data-page-id="{{ .RelPermalink }}"
  data-page-url="{{ .Permalink }}"
  data-page-title="{{ .Title }}"
></div>

<script async defer src="https://cusdis.com/js/cusdis.es.js"></script>
```


碰到的问题是，comment 系统太挤，Cusdis 是 iframe，默认很矮，需要手动拉才能看到完整评论。



要做的只有一件事。

在「h4」上面，加一段「style」，height 你可以根据需求自己调整。


```
<div style="margin: 50px 0;"> 

  <style>
  #cusdis_thread iframe {
    width: 100%;
    height: 800px;
    border: none;
  }
  </style>

  <h4>Comments:</h4>

  <div id="cusdis_thread"
    data-host="https://cusdis.com"
    data-app-id="b9de8ab5-52d3-45b6-8ad4-b7f4c7f4939b"
    data-page-id="{{ .File.UniqueID }}"
    data-page-url="{{ .Permalink }}"
    data-page-title="{{ .Title }}">
  </div>

  <script async defer src="https://cusdis.com/js/cusdis.es.js"></script>

</div>
```


