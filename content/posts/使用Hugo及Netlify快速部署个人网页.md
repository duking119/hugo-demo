---
title: "使用HUGO GITHUB NETLIFY 部署个人网页"
date: 2022-05-13T12:37:03+08:00
draft: false
cover:
    image: img/logo.jpg
    alt: 'This is a post image'
    caption: 'hugo fast and easy to use.'

tags: ["html","css"]
categories: ["tech"]
---

- 根据YouTube视频[Getting Started with Hugo](https://www.youtube.com/watch?v=hjD9jTi_DQ4&t=2197s) 学习记录
- 步骤一： 使用Hugo在本机构建静态网页项目
  - 安装hugo
    - 我使用的是Windows系统通过scoop安装hugo

    ```code
        # powershell install scoop
        > Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
        # Optional: Needed to run a remote script the first time
        > Invoke-WebRequest get.scoop.sh | Invoke-Expression

        #powershell install hugo
        > scoop install hugo       
    ```

    - 在建好的文件夹中启动power shell

    ```code
        # Hugo workflow        
        # 建立网站项目文件  使用yml 配置文件 代替默认的 .toml配置文件,yaml文件比toml文件更容易理解
        > hugo new site 'project name' -f yml
        # 转入项目文件夹中 
        > cd 'project name'
        # 在 https://themes.gohugo.io/ 中选择要使用的网站样式文件 并复制样式模板的GitHub 地址
        # 例如 hugo-PaperMod themes -->https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
        > git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
        # 打开 vscode程序
        > code .
        # 编辑项目目录中的config.yml 文件
            baseURL: "部署在netlify上个人网页的地址,开始时设为空"
            languageCode: en-us
            title: My new Hugo Site
            theme: PaperMod
            
            menu:
                main:
            - identifier: categories
                name: Categories
                url: /categories/
                weight: 10
            - identifier: tags
                name: Tags
                url: /tags/
                weight: 20
            - identifier: archives
                name: Archives
                url: /archives/
                weight: 30
        
        # 使用Hugo内置的网页预览, 预览地址默认为 //localhost:1313/
        > hugo server
        # 添加网页内容
            # create new post artical
        > hugo new posts/postname.md
        
    ```

    - 使用 markdown 语法编辑 .md files

    ```code
        --- # artical set
        title: "The First blog"
        date: 2022-05-13T12:37:03+08:00
        draft: false #define artical visable or hiden on website
        cover:  # cover images
            image: img/cover.jpg  # images store in 'static folder' sub folder
            alt: 'This is a post image'
            caption: 'This is the caption'
        
        tags: ["html","css"]
        categories: ["tech"]
        ---
        contents....
    ```
  
    - 所有配置选项都预制在特定的主题中，可以通过阅读主题的说明来改变网页的外观.

- 步骤二： 将项目同步至个人GitHub中
  - 初始化本机GitHub储存库

    ```code
        > git init 
        # initialize a Github repository in that folder 在文件夹中初始化一个Github储存库
    ```

  - 在项目文件中创建一个.gitmodules 文件,编辑内容

    ```code
        > [submodule "themes/PaperMod"]
        >    path = themes/PaperMod
        >    url = "https://github.com/adityatelange/hugo-PaperMod.git"
    
    ```

  - 上传到GitHub个人库中  #**issue** i can't display local image on webserver, and I change its URL from Github.
    ![gitpush img](https://raw.githubusercontent.com/duking119/hugo-demo/master/static/img/gitpush.jpg "使用vscode 自带的同步工具")

- 步骤三： 将netlify 与GitHub同步，部署个人网页
  - 注册一个Netlify账号
  - 选择Add new site
  - 链接GitHub账号，选择要共享的存储夹
  - 发布后复制个人网页地址，添入config.yml中的baseURL中
    ![netlify url](https://raw.githubusercontent.com/duking119/hugo-demo/master/static/img/address2.jpg "复制netlify网页的地址")
    ![base url](https://raw.githubusercontent.com/duking119/hugo-demo/master/static/img/address.jpg "补充到config.YML文件中")
  - 个人免费网页的初始部署已经基本完成了，后续可以修改网页的样式以及发布新的个人文章。
