---
title: Github pages 设置
---
Github pages 
# 目录结构
```
_config.yml          是配置文件，最为重要，包含了所有配置信息
_includes/           文件夹包含了将被反复利用的文件，比如footer，header
_layouts/            文件夹包含了主页面的排版布局
  |--  default.html  blog默认模板
_posts/              文件夹将包含所有的日志文件，Markdown格式
  |--  xxx.html  xxx.md ...  博客内容页
       注意，文件名必须为**"年-月-日-文章标题.后缀名"**的格式。
       例如： 2017-9-14-w1.md  
       github-url转化为: *http://git.tiqiule.cn/2017/09/14/w1.html*

```


# 实际测试（新添加）
## 修改页面布局
   可以选用官方的主题，比如：slate 。然后拷贝官方主题的 _layouts/default.html
，修改其中内容，比如去掉到项目主页的连接按钮，然后提交。

## 修改页面标题
>\---
>titile: my blog
>\---
也不用指定： layout:default  

## md文件转换为html
好像是自动转换的，比如/test.md 
如果访问域名 http://git.tiqiule.cn/test.md  就是没有渲染的原始文档
如果访问域名 http://git.tiqiule.cn/test.html 就是渲染后的页面(实际没有.html文件，自动生成)
.md 文件自动渲染  .html 不
git pull 获取远程关联库合并到本地更新


# 例子：模板 default.html 
```
<!DOCTYPE html>
　　<html>
　　<head>
　　　　<meta http-equiv="content-type" content="text/html; charset=utf-8" />
　　　　<title>\{\{ page.title \}\}</title>
　　</head>
　　<body>
　　　　\{\{ content \}\}
　　</body>
　　</html>
```


# 例子：博客内容页 xx.html or xx.md
>---
>layout: default
>title: 你好，世界
>---
<h2>\{\{ page.title \}\}</h2>
<p>我的第一篇文章</p>
<p>\{\{ page.date | date_to_string \}\}</p>


解释：
- 每篇文章的头部，必须有一个yaml文件头，用来设置一些元数据。它用三根短划线"---"，标记开始和结束，里面每一行设置一种元数据。

- "layout:default"，表示该文章的模板使用_layouts目录下的default.html文件；

- "title: 你好，世界"，表示该文章的标题是"你好，世界"

- category 设置文章的分类

- \{\{ page.title \}\}就是文件头中设置的"你好，世界"

- \{\{ page.date \}\}则是嵌入文件名的日期（也可以在文件头重新定义date变量）

- "| date_to_string"表示将page.date变量转化成人类可读的格式。


# 例子：网站首页 index.html
```
\---
layout: default
title: 我的Blog
\---
　　<h2>\{\{ page.title \}\}</h2>
　　<p>最新文章</p>
　　<ul>
　　　　\{\% for post in site.posts \%\}
　　　　　　<li>\{\{ post.date | date_to_string \}\} <a href="\{\{ site.baseurl \}\}\{\{ post.url \}\}">\{\{ post.title \}\}</a></li>
　　　　\{\% endfor \%\}
　　</ul>
```

- \{\% for post in site.posts \%\}，表示对所有帖子进行一个遍历。这里要注意的是，Liquid模板语言规定，输出内容使用两层大括号，单纯的命令使用一层大括号。

- \{\{site.baseurl\}\}就是_config.yml中设置的baseurl变量。


# 例子：分类列表
```
<h4>分类列表</h4>  
    <hr>  
    \{\% for category in site.categories \%\}  
    <li class="category_list_item"><a href="/showCategory.html?categoryName=\{\{ category | first \}\}">\{\{ category | first \}\}</a> (\{\{ category | last | size \}\})  
    </li>  
    \{\% endfor \%\}  
```
