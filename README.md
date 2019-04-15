# stevenshuang.github.io


## 使用的主题是[Yelee](https://github.com/MOxFIVE/hexo-theme-yelee.git)
## [Yelee使用手册](http://moxfive.coding.me/yelee/)

## 美化blog的一点建议
* [next主题下载](https://github.com/iissnan/hexo-theme-next)
* [鼎力推荐](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)
* [hexo next 文档](http://theme-next.iissnan.com/getting-started.html)
* [背景设置为一张图片](http://blog.csdn.net/qq_30242609/article/details/53440869)

## 常见操作
* 关于部分显示文章, 在主题的\_config.yml中找到auto_excerpt设置为true即可
* 设置左侧头像 在项目的根目录的配置文件\_config.yml设置一下, 两种形式:
  *  avatar: httpurl (直接引用网络的图片)
  *  avatar: /uploads/xxx.jpg (uploads位于source)
* 关于使用hexo g -d出现的Error解决方法. 切换到站点的根目录.
```bash
sudo npm install hexo-deployer-git --save
# mac下不需要sudo
```

## gitment的问题

1. gitment安装
```bash
npm install --save gitment
```

2. 在github创建app
> 主要的就是home url, 和callbalkurl，填写自己买的域名，或者是`https://username.github.io`

3. 配置git评论
> 在 `themes/yelee/layout/_partial/post/git.els`添加如下代码
> 其中gitment需要加载的js文件已经做了修改.
```html
<div id="git"></div>
<link rel="stylesheet" href="https://jjeejj.github.io/css/gitment.css">
<script src="https://jjeejj.github.io/js/gitment.js"></script>
<script>
var gitment = new Gitment({
  owner: "username",
  repo: "评论的仓库名称， 可以另建， 也可以直接使用username.github.io",
  oauth: {
    client_id: "**",
    client_secret:"**",
  },
})
gitment.render('git')
</script>
<!-- Gitment代码结束 -->
```

4. 在`themes/yelee/layout/_partial`下的article.els
```
<% if (!index){ %>
   <% if (post.comments){ %>
      <%- partial('post/git') %>
   <% } else { %>
      <div class="git"></div>
   <% } %>
<% } %>
```

5. 在根目录下的`themes/yelee/_config.yml`增加如下
```yml
gitment:
  enable: true
  count: true
  githubID: username
  repo: username.github.io 如果自己另建了仓库，写仓库的名字
  ClientID: *****
  ClientSecret: *****
  lazy: false
```

6. init comment
> 用自己的github登陆这个gitment， 初始化评论区.
> 接下来别人就可以评论了

7. gitment error:validation failed
> 造成这个问题的原因是，使用`issues`创建，会增加一个`gitment`, `article_path+article_title`, 会造成`label`过长， 导致出现该问题
> 所以在这里我才采取的解决办法是: 在根目录下的`_config.yml` 里更改`permalink`为`permalink: :year/:month/:day/:subtitle/`, 在每篇文章
> 的开头加上subtitle即可， 给每天的文章标号即可.1,2,3 ... , 新的一天还是从1开始标号，就不用考虑文章写的多， 导致数字过长的问题.
```
---
title: xxx
subtitle: 1
---
```

