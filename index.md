---
title: my blog new
---  
<p>最新文章:</p>
<ul>
　　　　{% for post in site.posts %}
　　　　　　<li>{{ post.date | date:%Y-%m-%d }}  <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
<hr>
　　　　{% endfor %}
</ul>
















