---
title: "Switch email and name for each Git repository"
date: 2021-05-22T20:41:56+09:00
draft: false
categories: ["Tech"]
tags: ["Git"]
---

Sometimes, I would like to switch `user.name` and `user.email` of git configuration. For example, I have two GitHub account, for business and for private. When I push some commits to repositories through the same laptop, name and email must be configured correctly for appropriate repository.  

In this case, we should set up user configuration for each repository. We can use below commands.

```bash
$ cd YOUR_REPOSITORY
$ git config --local user.name "hogehoge"                                                                                                                                                                                                      
$ git config --local user.email "hogehoge@example.com"  
```

If you have already modified user configuration in global setting, and you forget above commands, global settings apply. Preventing the careless mistake, we should configure bellow it.

```bash
$ git config --global --unset user.name
$ git config --global --unset user.email
$ git config --global user.useConfigOnly true
```

`user.useConfigOnly` forbid to commit without configuration of `user.name` and `user.email`. 

https://git-scm.com/docs/git-config#Documentation/git-config.txt-useruseConfigOnly
