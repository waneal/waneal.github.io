---
title: "Configure base image by argument"
date: 2021-05-27T22:52:27+09:00
draft: false
categories: ["Tech"]
tags: ["Docker"]
---


It is rare case, but sometimes I have to configure base image by command argument while executing `docker build`. For example, there are two AWS account, and I use base image contained in each ECR (Elastic Container Registry) for each account. Even I have two base image, but I should use only one Dockerfile. In this case, this solution help me.


- Dockerfile

```dockerfile
ARG BASE_IMAGE
FROM ${BASE_IMAGE}:latest
RUN hogehoge
```

- Command

```bash
$ docker build --build-arg BASE_IMAGE=XXXXXXXX.dkr.ecr.ap-northeast-1.amazonaws.com/baseimage .
```

`ARG` is the only  instruction that we can use before `FROM`

https://docs.docker.com/engine/reference/builder/#arg