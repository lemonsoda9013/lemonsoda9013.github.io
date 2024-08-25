# 说明

一个简单的静态个人主页，借助模板实现，可以低代码后续维护

## 基本信息

* 框架：[Hugo](https://gohugo.io/getting-started/quick-start/)

* 模板：[Digital Garden](https://digital-garden-hugo-theme.vercel.app/)

* 模板作者：[apvarun](https://apvarun.com/)

## 建站过程

### 新建Github仓库

* 新建一个Public仓库，Repository name设置为“自己的用户名.github.io”

* 在仓库设置中找到Pages，选择一个Branch，文件夹选择仓库根目录

* 可以通过“自己用户名.github.io”这个网址访问仓库中对应Branch的页面，网页文件放置在仓库根目录下

* 把这个仓库拉取到本地

### HUGO的使用

* 通过winget安装PowerShell（不是Windows自带的那个）和Hugo

* 打开PowerShell，用```hugo version```检查是否安装成功

* 切换到本地仓库的目录，执行```hugo new site -f```，创建网页的文件结构

* 使用```git submodule```或```git clone```下载模板，参照模板的文件结构把对应的文件复制到仓库根目录下（这一步可能与Hugo官方教程不同）

* 在仓库目录执行```hugo server```，点击窗口中的网址，可以在本地预览网页

### Digital Garden模板

* 模板的文件结构（忽略了一部分未使用的文件夹）

    ```
    .
    ├── ...
    ├── hugo.toml               # 对侧边栏进行控制
    ├── content                 # 储存所有Markdown文件的地方
    │   ├── _index.md           # 主页显示的内容
    │   └── articles            # 不可更改此文件夹名称
    │       ├── custom-1        # 分类名称和文章名称可以自定义
    │       │   ├── _index.md   # articles和以下的文件夹必须有
    │       │   ├── page-1.md
    │       │   └── page-2.md
    │       ├── custom-2
    │       │   ├── _index.md
    │       │   ├── page-1.md
    │       │   └── page-2.md
    │       ├── _index.md
    │       ├── page-1.md
    │       └── page-2.md
    └── ...
    ```
* 控制侧边栏
    ```
    title = "LEMONSODA9013" # 侧边栏左上角显示的内容

    [menu]                  # 侧边栏的菜单，weight决定上下顺序
    [[menu.main]]           # 可点击选项，需要指定名称和url
    name = 'Home'
    url = '/'
    weight = 1
    [[menu.main]]           # 不可点击，类型是标题
    name = 'Content'
    params.header = true
    weight = 2
    [[menu.main]]           # 标题下面的可点击选项
    name = 'All Articles'
    url = '/articles'       # 如果是外部链接右侧会显示一个小箭头
    weight = 3

    [[menu.social]]         # 侧边栏底部的社媒链接
    name = 'GitHub'
    url = 'https://github.com/lemonsoda9013'
    weight = 1
    ```
* Markdown文件结构
    ```
    # _index.md控制查看列表时顶部显示的文字
    ---
    title: All Articles
    ---

    # 其他md文件头部按下面格式设定标题和日期，图片可选
    ---
    title: 1. Theme Installation
    date: 2021-12-19
    images: 
    - https://raw.githubusercontent.com/apvarun/digital-garden-hugo-theme/main/images/digital-garden-logo.png
    ---
    （后接标题和正文）
    ```
    * content文件夹的_index.md可以后接标题和正文
    * articles文件夹的_index.md只能控制列表顶部文字
    * 再下层文件夹的_index.md可以添加图片，还可以后接内容做文字介绍
* 文章管理
    * 新建文件夹即添加类别（需要_index.md并且在侧边栏手动更新）
    * 新建Markdown文件即添加文章