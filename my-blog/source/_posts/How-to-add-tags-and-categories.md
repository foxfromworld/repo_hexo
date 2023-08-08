---
title: How to add tags and categories
date: 2023-08-08 19:11:59
tags: [Hexo, tags, categories]
categories: Hexo
---

## Execute below commands to add tags and categories

```
hexo new page categories
hexo new page tags
```

## Check the format of the new post in /scaffolds/post.md as below

```
---
title: {{ title }}
date: {{ date }}
tags:
categories:
---
```

# Try to add some tags and the category for the post

```
---
title: How to add tags and categories
date: 2023-08-08 19:11:59
tags: [Hexo, tags, categories]
categories: Hexo
---
```

## Disable comments in those pages.=

```
---
title: categories
type: categories
date: 2023-08-08 19:06:46
comments: false
---
```

```
---
title: tags
type: tags
date: 2023-08-08 19:05:58
comments: false
---
```