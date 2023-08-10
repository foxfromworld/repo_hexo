---
title: How to apply a new theme to Hexo
date: 2023-08-08 11:12:07
tags: [Hexo, theme, clean-blog]
categories: Hexo
---

## Download the theme

```
cd themes
git clone https://github.com/klugjo/hexo-theme-clean-blog.git clean-blog
```

## Remove the git related folder

## Modify the _config.yml under root directory and enable your new theme

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
#theme: landscape
theme: clean-blog
```

## Deploy your blog

```
hexo clean && hexo deploy
```