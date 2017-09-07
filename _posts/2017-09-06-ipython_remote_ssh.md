---
layout:     post
title:      How to remote use ipython notebook via ssh
date:       2017-09-05
summary:    This is a tutorial on how to run ipython notebook via ssh
categories: jekyll pixyll
---
## Run ipython notebook on remote machine
```
ssh user@host
```
```
ipython notebook --no-browser --port=8889

```
### Open terminal on your local machine

```
ssh -N -f -L localhost:8888:localhost:8889 user@host

```

### Open your website on your local machine
```
localhost:8888

```