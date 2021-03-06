# Docsify 非常优秀的 Markdown 文档阅读工具

感觉相当部分程序员都有写博客的习惯，说实话我自己确实没有这个方便的爱好，很多年前有一点兴趣。为此，自己还在很多年前开发一款博客程序。

[DYHB.BLOG-X](http://down.chinaz.com/soft/31194.htm)

用过自己写的 PHP 博客，还用过 Emlog、WordPress、Typecho 等等，始终没有能坚持下来。随着时间的推移，工作中经常有一些小的总结，一致都放到有道云笔记记录起来，遇到问题的时候可以快速查看。还是挺方便的。

后面的时候，用 hexo 来搭建静态网站放到 Github 上，部署起来也不是很麻烦，但是总感觉不够干净，每次写完都要执行一遍部署不安逸啊。也用过一段时间看云，感觉也不是很安逸。后面逛知乎的时候发现了这个 Docsify 这个文档神奇，一下子就感觉好极了。

## 超简单的安装

不需要生成一堆 HTML 静态文件，只需要一个 `index.html` 文件。最重要的是支持本地全文搜索，数据缓存到 localStorage 中，默认过期时间为一天。本地全文搜索，不需要像 hexo 通过 Algolia 来做全文搜索，这一点是最让我心动的功能。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>The book of Xiangmin Liu</title>
  <link rel="icon" href="_media/favicon.ico">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="keywords" content="doc,docs,documentation,gitbook,creator,generator,github,jekyll,github-pages,lxm">
  <meta name="description" content="A magical documentation generator.">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/vue.css" title="vue">
  <link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/dark.css" title="dark" disabled>
  <link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/buble.css" title="buble" disabled>
  <link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/pure.css" title="pure" disabled>
  <style>
    nav.app-nav li ul {
      min-width: 100px;
    }
  </style>
</head>

<body>
  <div id="app">Loading ...</div>
  <script>
    window.$docsify = {
      alias: {
        '/.*/_navbar.md': '/_navbar.md'
      },
      auto2top: true,
      coverpage: true,
      executeScript: true,
      loadSidebar: true,
      loadNavbar: true,
      mergeNavbar: true,
      maxLevel: 4,
      subMaxLevel: 2,
      ga: 'UA-106147152-1',
      name: 'HOME',
      search: {
        noData: {
          '/en-us/': 'No results!',
          '/': '没有结果!'
        },
        paths: 'auto',
        placeholder: {
          '/en-us/': 'search',
          '/': '搜索'
        }
      },
      formatUpdated: '{MM}/{DD} {HH}:{mm}',
      plugins: [
        function (hook, vm) {
          hook.beforeEach(function (html) {
            var url = 'https://github.com/hunzhiwange/notebook/blob/master/' + vm.route.file
            var editHtml = '[:memo: Edit Document](' + url + ')\n'

            return editHtml
              + html
              + '\n\n----\n\n'
              + '<a href="https://docsify.js.org" target="_blank" style="color: inherit; font-weight: normal; text-decoration: none;">Powered by docsify</a>'
          })
        }
      ]
    }
  </script>
  <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
  <script src="//unpkg.com/docsify/lib/plugins/search.min.js"></script>
  <script src="//unpkg.com/docsify/lib/plugins/ga.min.js"></script>
  <script src="//unpkg.com/docsify-pagination/dist/docsify-pagination.min.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-bash.min.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-markdown.min.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-nginx.min.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-php.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-sql.js"></script>
  <script src="https://unpkg.com/docsify-copy-code"></script>
</body>

</html>
```

!> 简洁的插件，往往只是添加一个 script 标签，非常酷。

## 自定义头部菜单

简单的自定义头部菜单，可以实现多国语言，特别适合软件国际化的需要，添加 `_navbar.md` 即可。

```markdown
- Translations
  - [:cn: 英文](/en-us/)
  - [:uk: 中文](/)
```

## 自定义侧边栏菜单

只需要简单地添加添加一个 `_sidebar.md` 即可。

```markdown
* First Level

  * [foo](bar.md)
```

## 自定义封面

进入首页首先进入一个封面，让你的笔记像一本书， 修改  `_coverpage.md` 即可。

```markdown
![logo](_media/logo.png)

# The book of Xiangmin Liu <small>1.0.0</small>

> 小牛仔学习笔记

* 左手代码
* 右手年华

[GitHub](https://github.com/hunzhiwange/notebook)
[Get Started](#HOME)
```

## 部署 Github Page

我推荐直接将代码上传到 Master 分支， 添加一个 `.nojekyll` 让 Github Page 允许访问 `_` 开发的 Markdown 文件就行。