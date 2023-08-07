---
title: How to embed images in Hexo posts
date: 2023-08-03 15:06:44
tags:
---

## Add lines below in _config.yml

```
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
```

After modifying _config.yml, create a new post and you will find a folder is created alone with the post.

```
hexo new post "My first page with an image"
```

Put the image inside the folder, and enbed the image with the file name as below. Deply the post. Bob's your uncle, you can see the image in the new post.

<script src="https://utteranc.es/client.js"
        repo="foxfromworld/utterances_comments"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>