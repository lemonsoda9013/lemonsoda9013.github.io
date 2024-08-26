# 说明

一个简单的静态个人主页，借助模板实现，可以低代码后续维护

>
> * [基本信息](#基本信息)
> * [建站过程](#建站过程)
>   * [新建网页仓库](#新建网页仓库)
>   * [HUGO的使用](#hugo的使用)
> * [后续维护](#后续维护)
>   * [模板的使用](#模板的使用)
>   * [文章管理](#文章管理)
> * [改动](#改动)
>   * [彩色文本](#彩色文本)
>

## 基本信息

* 服务：[Github Pages](https://pages.github.com/)

* 框架：[Hugo](https://gohugo.io/getting-started/quick-start/)

* 模板：[Digital Garden](https://digital-garden-hugo-theme.vercel.app/)

* 模板作者：[apvarun](https://apvarun.com/)

## 建站过程

### 新建网页仓库

* 新建一个Public仓库，Repository name设置为“自己的用户名.github.io”
* 在仓库设置中找到Pages，选择一个Branch，文件夹选择/docs，开启网页功能
* 现在可以通过“自己用户名.github.io”这个网址访问仓库中对应Branch的页面
* 如果没有网页文件，默认显示README.md

### HUGO的使用

* 通过winget安装PowerShell（不是Windows自带的）和Hugo
* 打开PowerShell，用```hugo version```检查是否安装成功
* 将某个目录作为根目录，执行```hugo new site -f```，在这个目录里创建生成网页所需的文件
* 使用```git submodule```或```git clone```下载模板，把模板文件放置在/themes下面
* 参照模板的文件结构把对应的文件复制到根目录下对应位置
* 在根目录执行```hugo server```，可以在本地实时预览并调试网页
* 在根目录执行```hugo```，在/public生成最终的网页文件
    * 如果Pages设置的文件夹是根目录，需要把/public里面的内容同步到仓库
    * 建议设置为/docs，可以同步整个目录，但是要把/public更名为/docs

## 后续维护

### 模板的使用

* Digital Garden模板的文件结构（忽略部分未使用文件夹）

    ```
    .
    ├── ...
    ├── hugo.toml               # 对侧边栏进行控制
    ├── content                 # 储存所有Markdown文件
    │   ├── _index.md           # 主页显示的内容
    │   └── articles            # 不可更改此文件夹名称
    │       ├── custom-1        # 分类和文章名称可以自定
    │       │   ├── _index.md   # 每层文件夹都应该有一个
    │       │   └── page-1.md
    │       ├── custom-2
    │       │   ├── _index.md
    │       │   └── page-2.md
    │       ├── _index.md
    │       └── page-3.md
    └── ...
    ```
* hugo.toml设置资源路径
    ```
    baseURL = "https://用户名.github.io/"   # 必须改成自己的网址
    ```
* 图片路径（生成的/public里面不会包含图片文件）
    ```
    https://raw.githubusercontent.com/用户/仓库/分支/images/文件
    ```
* hugo.toml控制侧边栏
    ```
    title = "LEMONSODA9013" # 侧边栏左上角显示的内容

    [menu]                  # 侧边栏菜单
    [[menu.main]]           
    name = 'Home'           # 显示的名称
    url = '/'               # 点击后跳转到的url
    weight = 1              # 决定上下顺序，依次增加，不可重复
    [[menu.main]]           
    name = 'Content'
    params.header = true    # 不可点击，类型是标题
    weight = 2
    [[menu.main]]           # 标题下面的可点击选项
    name = 'All Articles'
    url = '/articles'
    weight = 3

    [[menu.social]]         # 侧边栏底部的社媒链接
    name = 'GitHub'
    url = 'https://github.com/lemonsoda9013'
    weight = 1
    ```

### 文章管理

* 在/articles下新建文件夹和_index.md添加类别，侧栏需要添加对应选项
* _index.md文件结构
    ```
    ---
    title: All Articles
    ---
    ```
    * content文件夹的_index.md是主页内容， 可以后接标题和正文
    * articles文件夹的_index.md只能控制列表顶部文字
    * 再下层文件夹的_index.md可以添加图片，还可以后接内容做文字介绍
* 一般.md文件结构
    ```
    ---
    title: 1. Theme Installation
    date: 2021-12-19
    images: 
    - https://raw.githubusercontent.com/apvarun/digital-garden-hugo-theme/main/images/digital-garden-logo.png
    ---
    ```
    * 后接标题和正文
* 新建Markdown文件即添加文章

## 改动

### 彩色文本

原模板不支持在md文件中使用多色文字，因此修改了main.css，添加了新的类用于表示彩色文本，目前仅支持普通文字，支持颜色如下：

|HEX|示例|颜色名|
|:---:|:---:|:---|
|f44336|![f44336](https://via.placeholder.com/15/f44336/000000?text=)|red|
|e91e63|![e91e63](https://via.placeholder.com/15/e91e63/000000?text=)|pink|
|9c27b0|![9c27b0](https://via.placeholder.com/15/9c27b0/000000?text=)|purple|
|673ab7|![673ab7](https://via.placeholder.com/15/673ab7/000000?text=)|deeppurple|
|3f51b5|![3f51b5](https://via.placeholder.com/15/3f51b5/000000?text=)|indigo|
|2196f3|![2196f3](https://via.placeholder.com/15/2196f3/000000?text=)|blue|
|03a9f4|![03a9f4](https://via.placeholder.com/15/03a9f4/000000?text=)|lightblue|
|00bcd4|![00bcd4](https://via.placeholder.com/15/00bcd4/000000?text=)|cyan|
|009688|![009688](https://via.placeholder.com/15/009688/000000?text=)|teal|
|4bae4f|![4bae4f](https://via.placeholder.com/15/4bae4f/000000?text=)|green|
|8bc34a|![8bc34a](https://via.placeholder.com/15/8bc34a/000000?text=)|lightgreen|
|cddc39|![cddc39](https://via.placeholder.com/15/cddc39/000000?text=)|lime|
|ffeb3b|![ffeb3b](https://via.placeholder.com/15/ffeb3b/000000?text=)|yellow|
|ffc107|![ffc107](https://via.placeholder.com/15/ffc107/000000?text=)|amber|
|ff9800|![ff9800](https://via.placeholder.com/15/ff9800/000000?text=)|orange|
|ff5722|![ff5722](https://via.placeholder.com/15/ff5722/000000?text=)|deeporange|
|795548|![795548](https://via.placeholder.com/15/795548/000000?text=)|brown|
|9e9e9e|![9e9e9e](https://via.placeholder.com/15/9e9e9e/000000?text=)|grey|
|607d8b|![607d8b](https://via.placeholder.com/15/607d8b/000000?text=)|bluegrey|

使用方法如下：

```markdown
<p class="green">绿色文本</p>
```