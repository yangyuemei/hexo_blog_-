---
title: hexo博客开启评论功能
date: 2017-03-17 15:29:07
tags: hexo博客
category: hexo博客

---

# 主要步骤

1. 注册多说，得到shortname
2. 在博客根目录_config.yml  配置duoshuo_shortname:  yangyuemei
3. 在主题根目录_config.yml  配置duoshuo_shortname:  yangyuemei
4. 在artical.ejs文件中 替换一下内容

```java
	<% if (page.comment){ %>

<section id="comment">

  <h2 class="title">请点评：</h2>

<% if(theme.duoshuo_shortname) { %>

  	   <!-- 多说评论框 start -->

 		<div class="ds-thread" data-thread-key="<%- page.path %>" data-title="<%- page.title %>" data-url="<%- page.permalink %>"></div>

	<!-- 多说评论框 end -->
	<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
	<script type="text/javascript">
	var duoshuoQuery = {short_name:"yangyuemei"};   <!-- 替换这里的duoshuo_shortname为前面注册的shortname -->
		(function() {
			var ds = document.createElement('script');
			ds.type = 'text/javascript';ds.async = true;
			ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.unstable.js';
			ds.charset = 'UTF-8';
			(document.getElementsByTagName('head')[0] 
			 || document.getElementsByTagName('body')[0]).appendChild(ds);
		})();
		</script>
	<!-- 多说公共JS代码 end -->
	  <% } else if(config.disqus_shortname) { %>

  	 <div id="disqus_thread">
 <noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
   	 </div>

  <% } %>

</section>

<% } %>
```

