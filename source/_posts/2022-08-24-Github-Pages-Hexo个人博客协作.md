---
title: Github Pages+Hexo个人博客协作
date: 2022-08-24 16:31:09
tags: [Hexo,Github Pages]
---



下面将分享多设备之间进行个人博客维护的步骤，能够随时随地都能在不同的终端里面完成协作

### 1. 创建协作分支

由于 `hexo`  通过命令部署到 `github` 仓库的文件均为静态网页文件，仅用于 `github pages` 的展示，因此上传的分支是不包括配置文件上传的，需要重新创建一个新的分支，用于元数据的上传。



* 在 `github` 的博客仓库创建新的分支

```sh
git checkout -b 分支名称 #创建并切换至对应的分支
```

* 创建完分支后，把整个分支的代码都拉到本地里面

```sh
git clone -b <分支名称> <仓库地址>
```

---

### 2. 生成协作项目

创建好分支以后，需要把原本在本地的 `hexo` 项目的配置文件复制到创建好的 `git` 项目中，并对 `hexo` 项目进行初始化

* 复制本地项目的配置文件

下面是需要复制的文件结构

```bash
. # Hexo 项目根目录.
├─ _config.yml # Hexo 配置文件.
├─ _config.aurora.yml # Hexo Aurora 主题配置文件
├─ package.json # npm 已安装目录文件
├─ _source # 文章等静态资源
├─ scaffolds # 模版文件
└─ _config.aurora.yml # 主题配置.
```

* 复制完成后，安装所需要的插件

```sh
npm install
```

* 安装完插件以后，即可使用 `hexo` 的命令对项目进行初始化

```sh
hexo cl & hexo g
```

* 初始化完成后即可按照正常的 `git` 项目进行代码协作了

```sh
git add . 
git commit - m "first commit"
git push origin <分支名称>
```



> 搭建完成后，原来本地的项目可以删除了，只需要使用新建的项目进行 `hexo` 的初始化，以及 `git` 代码上传即可，这样就可以实现在不同设备间进行协作



### 3. 博客协作

搭建完成以后，协作就很简单了，只需简单的操作 `git` 命令，即可无缝衔接博客维护

```sh
git clone -b <分支名称> <仓库地址>
```

克隆完项目以后即可继续维护博客了