# 个人主页建立记录

## 方案

### 框架

[Hugo](https://gohugo.io/) 是一个开源的静态网站生成器，它能将 Markdown 格式的文本文件快速转化为可直接部署的静态网页。静态网页指的是不依赖后端服务器实时处理数据，仅通过 HTML、CSS、JavaScript 等前端文件就能展示内容的网页。

Hugo 社区提供了很多主题模板，这些模板定义了网站的整体布局和样式，以及如何从 Markdown 文件自动生成对应的网页文件。将生成的文件部署到 Web 服务器上，用户即可通过网址访问网站。

### 部署

GitHub Pages 是 GitHub 提供的静态网页托管服务。将包含网页文件的代码仓库推送到 GitHub，并指定对应分支和目录作为发布源，GitHub Pages 会自动将这些文件部署到用户专属的 ```github.io``` 域名下，即可实现网页的公开访问。

### 在线编辑

Codespace 是 GitHub 提供的云端开发环境，允许用户在浏览器中直接编写、运行和调试代码。在代码仓库的 Codespace 中安装 Hugo，即可在浏览器中对网站进行编辑和预览，无需在本地安装开发工具。

GitHub Action 是 GitHub 平台的自动化工具，能够在云端自动执行预设的工作流。用户可以将工作流设置为：当 Markdown 文件有更新时，自动生成新的静态网页文件，并将生成的文件推送至指定分支，即可实现网站的自动更新与部署。

## 前期准备

### 新建仓库

注册并登录 Github，在自己的 Github 页面上新建仓库，仓库名称可以设置为“自己的用户名.github.io”，仓库可见性设为 Public，其余配置保持默认。

### 配置本地环境

参考 Hugo 官方文档：[Hugo的安装与使用](https://gohugo.io/getting-started/quick-start/)

参考 Github 官方文档：[Git的安装与使用](https://docs.github.com/zh/get-started/git-basics/set-up-git)

安装 Git 后，将仓库克隆到本地，即可在本地进行开发。

需要至少看懂并掌握以下的 Git 命令：

* ```git clone 仓库URL```
* ```git add .```
* ```git commit -m "提交说明"```
* ```git push origin main```

### 配置Codespace

在仓库页面可以为仓库开通 Codespace。Codespace 实际上是由 Github 提供的虚拟机，启动 Codespace 时，Github 会在浏览器中开启一个连接到该虚拟机的网页版 VSCode。

Codespace 可以免费使用，但是有使用时间和容量上的限制。对于最基础的 2 核心虚拟机，免费用户每个月最多可以使用 60 小时，且虚拟机占用的存储空间不能超过 15 GB。( 安装Hugo之后约为 12 GB )

可以在启动 Codespace 后手动安装 Hugo，也可以提前在仓库中上传配置文件，在启动 Codespace 时自动安装 Hugo。

配置文件的路径：```.devcontainer/devcontainer.json```

```json
{
  "name": "Hugo Dev Environment",
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu", 
  "features": {
    "ghcr.io/devcontainers/features/hugo:latest": {
      "version": "latest",
      "extended": true
    }
  },
  "postCreateCommand": "hugo version"
}
```

## Hugo的使用方法