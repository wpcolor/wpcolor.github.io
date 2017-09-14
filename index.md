---
title: my blog
---  


<p>最新文章</p>
<ul>
　　　　{% for post in site.posts %}
　　　　　　<li>{{ post.date | date_to_string }} {{ post.title }}</li>
　　　　{% endfor %}
</ul>
















