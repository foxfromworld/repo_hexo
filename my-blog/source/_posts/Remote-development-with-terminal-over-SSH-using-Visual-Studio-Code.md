---
title: Remote development with terminal over SSH using Visual Studio Code
date: 2023-08-03 18:23:56
tags:
---

### Enable SSH on the server

```
sudo apt update
sudo apt install openssh-server
```

### Install the extension in Visual Studio Code

![](extension.png)

### After installing the extension, the green button and the new status bar will appear at the bottom left.

![](connection.png)

### Click on the green button to connect to a new host.

![](Connect2Host.png)

### Enter the command to connect to the server.

Example: ssh username@ip

![](NewHost.png)

### Save the config

![](config.png)

### Connect to the host via the pop-up or the green button.

![](connect.png)

### Input the password to establish the connection (every time).

![](password.PNG)

<script src="https://utteranc.es/client.js"
        repo="foxfromworld/utterances_comments"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>