---
title: Github Pages + Hexo 个人博客搭建分享
date: 2022-08-16 17:11:11
tags: [Hexo,Github Pages]
---

**本文将给大家分享个人博客搭建的详细步骤，以及搭建过程中踩到的坑，希望能够帮助大家快速搭建自己的博客，能够记录开发过程中遇到的问题和总结出的经验。**

*博主选的是 Github Pages + Hexo + Aurora主题，如果是自己有时间和兴趣去写动态网页的博客，需要自己购买服务器和域名比较麻烦，还是比较推荐直接用现成静态网页去做比较好，省时省力也省钱，也能满足绝大部分功能了*

**准备工作:** *Node.js  Git 搭建博客依赖的环境*

*Hexo Doc: https://hexo.io/zh-cn/docs/*



### 1.  站点选型

> Github Pages

​		由于Github是国外站点，没有梯子时不时都会抽风，但Github有个好处是申请Github Pages不需要上传自己身份证信息(我就是因为太懒不想上传哈哈)，如果不想折腾，能接受有时候蜗牛一样的访问速度，推荐使用Github Pages。下面是Github Pages的整合步骤。

1. 创建 Github 仓库

![创建仓库](./2022-08-16-Github-Pages-Hexo-个人博客搭建分享/github仓库创建.jpg)

看网上大部分文章都说仓库名命名如果是 {github用户名}.github.io ，仓库就会自动开启 github pages，仓库名直接用github用户名好像也可以(可以试试)，这样访问github pages的时候域名直接就可以用 {github用户名}.github.io 访问，否则就要在域名后面加上仓库名称才能访问自己的博客

2. 设置 github pages

![设置](./2022-08-16-Github-Pages-Hexo-个人博客搭建分享/gitpage页面.jpg)

* 如果是用用户名创建了仓库，直接访问上述的域名即可，如果是自己有申请独立域名，可以在下方的 Custom domain设置自定义域名

* 同时可以选择自己编译后的静态网页部署在哪个分支，可以在 Branch 选项设置分支，以及保存的根目录路径

> Gitee Pages

​		Gitee Pages 其实和 Github Pages 的区别不大，博主本来也是打算用 Gitee 来搭建的，但是之前没有现成的身份证正反面以及手持身份证的照片，就没选择这种方式。

1. 创建 Gitee 仓库

![创建仓库](./2022-08-16-Github-Pages-Hexo-个人博客搭建分享/gitee仓库创建.jpg)

和 Github 一样，以用户名作为仓库的名称，创建一个存放静态网页文件的仓库

2. 开启 Gitee Pages 功能

在 *服务* 菜单里面开启 Gitee Page 功能，如果之前没有做过实名认证，是需要上传身份证资料的，根据自己的情况选择是不是要上传，不实名认证是无法开启这个功能的

![实名认证](./2022-08-16-Github-Pages-Hexo-个人博客搭建分享/实名认证.jpg)

---

### 2. Hexo

> 安装步骤

*Hexo* 利用 *Node.js* 和  *NPM* 安装比较方便，在安装前需前往 *Node.js* 官网先安装好环境，同时需要安装 *Git*

#### 2.1 npm 安装 Hexo

在自己的项目目录里面创建一个文件夹用来保存 Hexo 项目，安装好 Node npm 和 Git 环境后，执行安装命令

``` shell
npm install hexo --save
```

执行完成后可以执行命令查看版本，执行看到有 *hexo-cli* 的版本号就说明成功安装了

```shell
hexo -version
```

安装 *hexo git* 的插件

 ```shell
npm install hexo-deployer-git --save
 ```

初始化 hexo 项目，后面上传的文件夹就是初始化后的目录

```shell
hexo init <要创建的目录名称>
```

进入到刚才创建的项目目录里面,安装所有依赖的包

```shell
npm install
```

安装完成后，可以看到目录结构如下图

![目录结构](./2022-08-16-Github-Pages-Hexo-个人博客搭建分享/目录结构.jpg)

执行以下 hexo 的命令，即可在本地生成静态网页文件并运行

```shell
#清空hexo所有已经生成的静态网页文件，如果修改了 yaml 配置文件一定要先执行此命令清空
hexo clean 
#也可以简写成
hexo cl
```

执行完清理命令后，需要执行生成静态网页文件的命令

```shell
#生成静态网页文件
hexo generate
#也可以简写成
hexo g
```

生成完成后，可以现在本地运行，运行成功后访问 https://localhost:4000 访问本地博客，也可以指定运行的端口，看自己需求

```shell
#不指定端口运行，默认4000端口启动
hexo server
#也可以简写成
hexo s
#如果需要指定端口，则执行以下命令
hexo server -p 8000
#简写也是可以的
hexo s -p 8000
```

#### 2.2 主题安装

默认的主题是真的很默认，可以自行到 Hexo 官网的主题库中挑选自己喜欢的主题，我选的是三钻的 Aurora 主题，能用 npm 安装而且有自己的主题文档，十分方便，而且确实很好看，第一眼就被吸引了。

*Hexo 主题库: https://hexo.io/themes/*

*Aurora Doc*: https://aurora.tridiamond.tech/zh/guide/

下面我以 Aurora 为例安装主题，可能有部分主题不支持 npm 安装，需要手动保存文件夹再做处理，具体可以根据选择的主题文档完成安装操作

1. 在控制台中，进入 Hexo 项目的根目录，执行主题安装命令

```shell
npm install hexo-theme-aurora --save
```

2. 因为主题是使用 NPM 或者 Yarn 安装的，而不是 clone 到 themes 文件夹的。所以我们需要自己创建一个配置文件。你只需要在 Hexo 博客的根目录下创建一个 `_config.aurora.yml` 配置文件来配置主题

```shell
#命令 windows powershell 不支持，需自行在 下面的路径中找到文件后直接复制
cp -rf ./node_modules/hexo-theme-aurora/_config.yml ./_config.aurora.yml
```

3. 设置*permalink*

