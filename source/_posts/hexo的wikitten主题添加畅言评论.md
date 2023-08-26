---
title: hexo的wikitten主题添加畅言评论
toc: true
date: 2023-08-26 1:48:20
tags: 
	- hexo
	- 主题
categories:
	 - web
	 - hexo
---

先看wiki网站 [芝士就是C](https://wiki.94c.cn)

## 一、快速开始

### 1.注册畅言，根据提示操作
##### 获取安装代码[推荐选择-自适应安装代码]

``` javascript
<!--PC和WAP自适应版-->
<div id="SOHUCS" sid="请将此处替换为配置SourceID的语句" ></div> 
<script type="text/javascript"> 
(function(){ 
var appid = '******'; 
var conf = '******'; 
var width = window.innerWidth || document.documentElement.clientWidth; 
if (width < 1000) {
var head = document.getElementsByTagName('head')[0]||document.head||document.documentElement;
var script = document.createElement('script');
script.type = 'text/javascript';
script.charset = 'utf-8';
script.id = 'changyan_mobile_js';
script.src = 'https://cy-cdn.kuaizhan.com/upload/mobile/wap-js/changyan_mobile.js?client_id=' + appid + '&conf=' + conf;
head.appendChild(script);
} else { var loadJs=function(d,a){var c=document.getElementsByTagName("head")[0]||document.head||document.documentElement;var b=document.createElement("script");b.setAttribute("type","text/javascript");b.setAttribute("charset","UTF-8");b.setAttribute("src",d);if(typeof a==="function"){if(window.attachEvent){b.onreadystatechange=function(){var e=b.readyState;if(e==="loaded"||e==="complete"){b.onreadystatechange=null;a()}}}else{b.onload=a}}c.appendChild(b)};loadJs("https://cy-cdn.kuaizhan.com/upload/changyan.js",function(){window.changyan.api.config({appid:appid,conf:conf})}); } })(); </script>
```

### 2.themes/Wikitten/layout/comment下新建changyan.ejs
注意：
要把`<div id="SOHUCS" sid="请将此处替换为配置SourceID的语句" ></div>`代码去除掉！
``` bash
cd themes/Wikitten/layout/comment
vim changyan.ejs 
```
``` javascript
<!--PC和WAP自适应版-->
<script type="text/javascript">
(function(){
var appid = 'cyujNvB7y';
var conf = 'prod_3af86b3f282c22e7ff32d9c6d3337b54';
var width = window.innerWidth || document.documentElement.clientWidth;
if (width < 1000) {
var head = document.getElementsByTagName('head')[0]||document.head||document.documentElement;
var script = document.createElement('script');
script.type = 'text/javascript';
script.charset = 'utf-8';
script.id = 'changyan_mobile_js';
script.src = 'https://cy-cdn.kuaizhan.com/upload/mobile/wap-js/changyan_mobile.js?client_id=' + appid + '&conf=' + conf;
head.appendChild(script);
} else { var loadJs=function(d,a){var c=document.getElementsByTagName("head")[0]||document.head||document.documentElement;var b=document.createElement("script");b.setAttribute("type","text/javascript");b.setAttribute("charset","UTF-8");b.setAttribute("src",d);if(typeof a==="function"){if(window.attachEvent){b.onreadystatechange=function(){var e=b.readyState;if(e==="loaded"||e==="complete"){b.onreadystatechange=null;a()}}}else{b.onload=a}}c.appendChild(b)};loadJs("https://cy-cdn.kuaizhan.com/upload/changyan.js",function(){window.changyan.api.config({appid:appid,conf:conf})}); } })(); </script>
```
### 3.themes/Wikitten/layout/comment下修改counter.ejs
注意：
我直接把disqus关键词替换成changyan，class中的我没动，若你不喜欢可以删除掉disqus-comment-count
``` javascript
<% if (post.comments) { %>
    <% if (theme.comment.changyan) { %>
        <a href="<%- post.permalink %>#comments" class="article-comment-link disqus-comment-count"><%= __('article.comments') %></a>
    <% } else if (theme.comment.duoshuo) { %>
        <a href="<%- post.permalink %>#comments" class="article-comment-link ds-thread-count" data-thread-key="<%= post.permalink %>"><%= __('article.comments') %></a>
    <% } else if (theme.comment.youyan) { %>
        <a href="<%- post.permalink %>#comments" class="article-comment-link"><%= __('article.comments') %></a>
    <% } %>
<% } %>
```
### 4.themes/Wikitten/layout/comment下修改index.ejs
注意：
找到关键词changyan的3行
``` javascript
<% if (post.comments) { %>
    <% if (theme.comment.changyan) { %>
        <section id="comments"> <%- partial('common/post/changyan') %> </section>
        <section id="comments"> <%- partial('comment/changyan') %> </section>
    <% } else if (theme.comment.duoshuo) { %>
        <section id="comments"> <%- partial('comment/duoshuo') %> </section>
    <% } else if (theme.comment.youyan) { %>
        <section id="comments"> <%- partial('comment/youyan') %> </section>
    <% } %>
<% } %>
```
### 5.themes/Wikitten/layout/comment下修改script.ejs
注意：
找到关键词changyan的2行
``` javascript
<% if (theme.comment.changyan) { %>
    <%- partial('comment/changyan', { script: true }) %>
<% } else if (theme.comment.duoshuo) { %>
    <%- partial('comment/duoshuo', { script: true }) %>
<% } else if (theme.comment.youyan) { %>
    <%- partial('comment/youyan', { script: true }) %>
<% } %>
```
### 6.themes/Wikitten/layout/common/post下新增changyan.ejs
写入下面代码
``` javascript
<div id="SOHUCS" sid="<%= post.title %>" ></div>
```
### 7.themes/Wikitten/下修改_config.yaml
注意：
changyan: 随便给个真值就行
``` javascript
comment:
    changyan: 94c管理员 # enter disqus shortname here
    duoshuo: # enter duoshuo shortname here
    youyan: # enter youyan uid here
```
### 8.大功告成
点击 [芝士就是C](https://wiki.94c.cn)
## 二、参考资料
> - [hexo的tranquilpeak配置畅言](https://blog.csdn.net/chenhong7232/article/details/100789474)
> - [sourceid配置](https://changyan.kuaizhan.com/static/help/f-source-id.html)
