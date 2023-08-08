---
title: How to add a comment system to Hexo
date: 2023-08-07 15:04:28
tags:
---

## Create a public repository to store install the comment system.

https://github.com/foxfromworld/utterances_comments

## In stall the Utterances comment system to the repository which was just created.

https://github.com/apps/utterances

Install Utterances in the selected repository.

![](Install.png)

## Enter your settings on the webpage and copy the generated script snippet.

https://utteranc.es/

```
<script src="https://utteranc.es/client.js"
        repo="foxfromworld/utterances_comments"
        issue-term="url"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
```

## Try leaving your message

![](comment.PNG)

![](permission.PNG)

![](test.PNG)

## Ummm...The function is not working properly. I left one message under one post and it's appearing on every post.

So I changed issue-term from "url" to "pathname" and the problem is still there...

## I applied a new theme to my blog

Add this setting to my-blog/themes/clean-blog/_config.yml

```
utterances:
  enable: true
```

Addd the snippet to my-blog/themes/clean-blog/layout/_partial/comments.ejs

```
<div class="comments" id="comments">
<script src="https://utteranc.es/client.js"
    repo="foxfromworld/utterances_comments"
    issue-term="pathname"
    theme="github-light"
    crossorigin="anonymous"
    async>
</script>
</div>
```

## Deploy your blog

```
hexo clean && hexo deploy
```