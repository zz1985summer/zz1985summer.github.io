---
title: To deploy hexo blog
abbrlink: 46497
date: 2017-12-21 09:20:41
tags:

---

# 部署环境
首先 hexo 部署需要 nodejs 和 git 分别安装这两个环境工具


# 安装 hexo
进入想部署的 blog 路径

```
npm install hexo-cli -g

hexo init <folder>
cd <folder>
npm install

hexo g
hexo s

浏览器访问:
http://localhost:4000

```
# 安装相关插件
```
npm install hexo-generator-index --save
npm install hexo-generator-archive --save
npm install hexo-generator-category --save
npm install hexo-generator-tag --save
npm install hexo-server --save
npm install hexo-deployer-git --save
npm install hexo-deployer-heroku --save
npm install hexo-deployer-rsync --save
npm install hexo-deployer-openshift --save
npm install hexo-renderer-marked@0.2 --save
npm install hexo-renderer-stylus@0.2 --save
npm install hexo-generator-feed@1 --save
npm install hexo-generator-sitemap@1 --save
```
# 配置hexo
打开 hexo 安装路径下 _config.yml
站点标题等看字段相应编辑
这里需要注意,字段:后注意有一个空格

其中
```
deploy:
  type: git
  repo: <仓库git地址或者HTTPS地址>
  branch: master
```
是配置 github 的
# 发布新文章
```
hexo new "title"
```
# 部署 启动  
``` 
hexo g   //生成静态文件  
hexo d   //部署  

启动本地服务器  
hexo s  
在浏览器中运行: http://localhost:4000  
```


# 遇到的坑
部署 Hexo 博客到 Github Pages 时遇到的一个坑

1.当 使用 git 仓库部署时

```
fatal: 'github.com' does not appear to be a git repository
fatal: Could not read from remote repository.
Please make sure you have the correct access rights
and the repository exists.
```

2.当使用 HTTPS 仓库 部署时

```
Error: bash: /dev/tty: No such device or address
error: failed to execute prompt script (exit code 1)
fatal: could not read Username for 'https://github.com': Invalid argument
```

解决方法

使用带用户名和密码的 HTTPS 链接 

```
https://<yourusername>:<yourpwd>@github.com/zz1985summer/zz1985summer.github.io.git  
```  


