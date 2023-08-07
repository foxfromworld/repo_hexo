---
title: How to create a blog using GitHub Pages
date: 2023-07-31 19:43:04
tags:
---

## Step by step

### Create a repository for blog

Repository name: [foxfromworld.github.io](https://github.com/foxfromworld/foxfromworld.github.io)

### Create a repository for storing the content of the blog

Repository name: [repo_hexo](https://github.com/foxfromworld/repo_hexo)

### Clone the git repository

```
$ git clone https://github.com/foxfromworld/repo_hexo.git
```

### Install nmp (Node Package Manager)

```
sudo apt install npm
```

### Install Hexo

```
npm install hexo -g
```

If you encounter the error below...

```
npm ERR! node v8.10.0
npm ERR! npm  v3.5.2
npm ERR! code EMISSINGARG
npm ERR! typeerror Error: Missing required argument #1

```

Please follow below steps to fix the issue.

```
sudo apt-get remove nodejs
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
source ~/.profile
nvm install 16
```

### Initialize the blog

```
hexo init folder
```

If you encounter the error below...

```
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: target not empty
```

Initialize the blog in another empty folder.

```
hexo init my-blog
```

Create a new post.

```
hexo new post "My first page by Hexo"
```

Try to test and run server locally at http://localhost:4000/

```
hexo server
```

### Deploy the blog

edit _config.yml

Enter the info in the Deployment section.
```
deploy:
   type: git
   repo: git@github.com:foxfromworld/foxfromworld.github.io.git
   branch: master
```


```
npm install hexo-deployer-git --save
hexo clean && hexo deploy
```

If you encounter the error below, please follow below steps to set up the ssh connection.

```
FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/docs/troubleshooting.html
Error: Spawn failed
```

```
git config --global user.name <your user name>
git config --global user.email <your email>
ssh-keygen -t rsa -C <your email>
# Add your key on GitHub and test the connection
ssh git@github.com
```

If you see the following messages, that means your connection is setup correctly.

```
PTY allocation request failed on channel 0
Hi foxfromworld! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

After one or two minutes, the blog will be available.

Check https://github.com/foxfromworld/foxfromworld.github.io/settings/pages.

It takes longer time for the first time. You should be able to see "Your site is live at https://foxfromworld.github.io/", when the blog is available.

### Push all the changes

https://github.com/foxfromworld/repo_hexo/tree/main/my-blog

<script src="https://utteranc.es/client.js"
        repo="foxfromworld/utterances_comments"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>