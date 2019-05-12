# 如何搭建自己的技术博客
> 2019.05.11 by wushifei

## 安装
1.依赖环境：node8.0已上版本，可在[node官网](https://nodejs.org/zh-cn/)安装。    
&nbsp;&nbsp;&nbsp;查看node版本:
``` js
~ node -v

v8.12.0
```

2.安装VuePress
打开终端，输入如下命令：
``` js
~ npm install -g vuepress

http fetch GET 200 https://registry.npm.taobao.org/caniuse-db/download/caniuse-db-1.0.30000909.tgz 3993ms
/usr/local/bin/vuepress -> /usr/local/lib/node_modules/vuepress/bin/vuepress.js
+ vuepress@0.14.5
removed 1 package and updated 13 packages in 68.944s
```
查看vuepress安装的位置和版本
``` js
~ where vuepress
/usr/local/bin/vuepress
➜  ~ vuepress --version
0.14.5
```
## 启动一个服务
1.终端创建一个文件夹，并创建一个md文件：
``` js
~ mkdir docs
~ cd docs
// 创建一个md文件
~ echo '# vuepress' > README.md
```
若出现乱码，手动将文件改成'UTF-8'格式。

2.创建配置文件package.json
``` json
~ cd docs
// 生成package.json文件
~ npm init -y
// 配置"script"
{
  "name": "docs",
  "version": "1.0.0",
  "description": "fsdjfosdifjjk",
  "main": "index.js",
  "scripts": {
    "dev": "vuepress dev .",
    "build": "vuepress build .",
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

3.本地启动服务开发
``` js
~ npm run dev // 或 vuepress dev . 


 WAIT  Extracting site metadata...

 DONE  [00:34:16] Build 94707d finished in 5175 ms!

> VuePress dev server listening at http://localhost:8080/
```
此时在浏览器中输入[http://localhost:8080]就能浏览效果了。
## 配置文件说明
配置需要在文档目录下创建一个.vuepress目录，所有vuepress相关的文件都将会被放在这里。
创建文件夹：
``` js
mkdir .vuepress
```
其中最重要的文件.vuepress/config.js，网站的所有文件的配置都在这个文件里面，该文件需要导出一个js对象，.vuepress/public放置静态资源：
``` js
module.exports = {
    title: '阿飞日志',
    description: '吴士飞的日志',
    base: 'docPage',
    repo: 'https://github.com/TaoXuSheng/mt-blog' // 添加 github 链接
    head:[
        ['link',{rel:'icon',href:'/imgs/icon.ico'}],
    ],
    themeConfig: {
        nav:[
            { text: '主页', link: '/' },
            { text: '随笔', link: '/essay/vuepress.md' },
            { text: '框架', items: [
                { text: 'Vue',link: '/frames/vue/initVue.md' },
                { text: 'React', link: '/frames/React/initReact.md' }
            ]}
        ],
        sidebar: {
                '/essay/': [ 'vuepress', 'MarkDown' ],
                '/frames/vue/': [ "initVue", 'axios', 'vuex' ],
                '/frames/React/': [ 'initReact' ]
            },
        sidebarDepth: 2,
        lastUpdated: 'Last Updated',
        
    }
}
```
+ title：网站标题

+ description：网站描述

+ head：额外的需要被注入到当前页面的HTML<head></head>标签中，其中路径的'/'就是public资源目录。

+ nav：导航栏配置，此配置主要用于配置导航栏的连接，例如已上主页的link为'/',默认是根目录下的README.md。'/essay/'会默认链接到essay目录下的README.md文件。

+ sidebar：侧边栏配置，你可以省略.md拓展名，同时以/结尾的路径将会被视为 */README.md。'/vue/'、'/react/'是通过路由的方式将每个页面的标题抽取出来显示。

+ sidebarDepth：嵌套的标题链接深度，默认的深度为1。

+ lastUpdated：最后更新时间。

+ VuePress 默认将文件打包在 .vuepress/dist目录下，我们可以通过 dest属性修改文件输出目录，例如将文件输出在项目根目录下的 dist文件夹中。
通过设置 repo属性，VuePress 会在导航栏中添加一个 Github 仓库的链接。

+ 在使用 VuePress 编写博客并发布到 Github pages 的时候，我们可能会遇到下图所显示的问题，页面已经有了，但是样式和 js 没有加载成功。我们可以通过配置 base 属性来解决这个问题， base 属性的默认值是 /。假如您准备将代码部署到 taoxusheng.github.io/mt-blog/ , 那么 base属性就应该被设置成 /mt-blog/。注意：base 属性的值总是以 / 开始并以 / 结束。
![error](/docPage/imgs/error.png)

具体的配置请参阅[文档](https://vuepress.vuejs.org/zh/config/#%E5%9F%BA%E6%9C%AC%E9%85%8D%E7%BD%AE)

## 首页设置

vuepress内置了一个主页样式，是Front-matter格式的，[Front-matter教程](https://hexo.io/zh-cn/docs/front-matter)
首页的文件是根级README.md文件，在文件中写入如下配置：
``` js
home: true
heroImage: 
actionText: 快速上手 →
actionLink: /zh/guide/
features:
- title: 简洁至上
  details: 以 Markdown 为中心的项目结构，以最少的配置帮助你专注于写作。
- title: Vue驱动
  details: 享受 Vue + webpack 的开发体验，在 Markdown 中使用 Vue 组件，同时可以使用 Vue 来开发自定义主题。
- title: 高性能
  details: VuePress 为每个页面预渲染生成静态的 HTML，同时在页面被加载的时候，将作为 SPA 运行。
```

## 部署

1.在 docs/.vuepress/config.js 中设置正确的 base。    
2.git上建立一个仓库。    
![1](/docPage/imgs/1.png)

![2](/docPage/imgs/2.png)

3.在你的项目中，创建一个如下的 deploy.sh 文件（请自行判断去掉高亮行的注释）:
``` js

#!/usr/bin/env sh

# 确保脚本抛出遇到的错误
set -e

# 生成静态文件
npm run docs:build

# 进入生成的文件夹
cd docs/.vuepress/dist

# 如果是发布到自定义域名
# echo 'www.example.com' > CNAME

git init
git add -A
git commit -m 'deploy'

# 如果发布到 https://<pre><USERNAME></pre>.github.io
# git push -f git@github.com:<pre><USERNAME></pre>/<pre><USERNAME></pre>.github.io.git master

# 如果发布到 https://<pre><USERNAME></pre>.github.io/<pre><REPO></pre>
# git push -f git@github.com:<pre><USERNAME></pre>/<pre><REPO></pre>.git master:gh-pages

cd -
```
4.执行脚本文件完成发布
``` js
bash deploy.sh
```

5.在你项目的根目录下创建一个名为 .gitlab-ci.yml 的文件，无论何时你提交了更改，它都会帮助你自动构建和部署：
``` js

image: node:9.11.1

pages:
 cache:
   paths:
   - node_modules/

 script:
 - npm install
 - npm run docs:build
 artifacts:
   paths:
   - public
 only:
 - master
```
