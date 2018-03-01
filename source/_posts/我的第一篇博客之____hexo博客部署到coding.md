---
title: hexo博客部署到coding
date:  2017-03-16 17:01:41
tags: hexo博客
category:  hexo博客

---

1. **安装node.js 环境，用命令行工具node -v  npm -v检测是否安装成功**

2. **安装` git ` 环境，用命令行工具`git --version` 检测是否安装成功**

3. **git全局配置：**

   * `git config --global user.name "your name" `
   * git config --global user.name "your email;" `


4. **注册coding账号并登陆,新建项目比如:myblog  **

   * 切换到pages->部署来源选master分支

5. **配置 sshkey**

   * 使用命令工具  `ssh-key -t rsa -C "your@com"`
   * 一般在c盘打开.ssh->id_rsa.pub  复制里面全部的内容到coding找到ssh粘贴添加即可
   * 测试ssh是否添加成功，`ssh -T git@git.coding.net`,出现hi ，‘你的姓名就是成功

6. **安装hexo**

   * `npm install -g hexo`
   * `npm install hexo --save`
   * 看看hexo是否安装成功  `hexo -v`

7. **随便在本地的一个地方新建一个文件夹hexo，进入到它的根目录，右键 Git Bash Here 进入**

8. **初始化hexo ：`hexo init`**

9. **npm 自动安装需要的组件：`npm install`**

10. **生成 `hexo g`**

11. **启动 `hexo d`**

12. **若端口冲突。则hexo server -p 5000**

13. **到此为止，hexo在本地的配置已经完成了**





修改 _config_yml文件

* url ：“yourname.coding.me”
* root：/你在coding建的仓库名/

repository  即为ssh地址



​    **deploy:**

​         **type:git**

​         **repository:git@git.coding.net:yourname/yourcodingname.git**   

​         **branch:master**



**`hexo d` push到coding**

**hexo push常用命令**

1. `hexo clean`
2. `hexo g`
3. `hexo d`
4. `hexo s ` 本地预览