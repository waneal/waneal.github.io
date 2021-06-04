---
title: "Debug CodeBuild with custom image"
date: 2021-06-04T22:34:50+09:00
draft: false
categories: ["Tech"]
tags: ["AWS", "CodeBuild", "Docker"]
---

AWS CodeBuild is managed service for helping continuous integration and deployment. In CodeBuild, we normally use managed container image provided Amazon, it contains almost runtimes like android, dotnet, golang and more. We're usually satisfied the managed image, but sometimes need to use custom image you build, CodeBuild can run on it.

When debugging in CodeBuild, we can log in the container running by codebuild, it's very convenience. To use the function, we set `codebuild-breakpoint` in buildspec file. This function's mechanism is based on SSM agent. [Official document](https://docs.aws.amazon.com/codebuild/latest/userguide/session-manager.html) tell you it in detail.

Managed container image already has preparation for ssm agent, but custom image needs to install SSM agent and configure it. Below sample Dockerfile is what this is the case of using Amazon Linux 1 in Codebuild.

```dockerfile
FROM amazonlinux:1

# set your creation, this is sample
RUN yum update && yum install -y mysql-devel git bzip2 gcc openssl-devel readline-devel zlib-devel gcc-c++ postgresql-devel zip

# setup ssm-agent
RUN yum install -y https://s3.ap-northeast-1.amazonaws.com/amazon-ssm-ap-northeast-1/latest/linux_amd64/amazon-ssm-agent.rpm
RUN curl https://raw.githubusercontent.com/aws/aws-codebuild-docker-images/master/ubuntu/standard/4.0/amazon-ssm-agent.json > /etc/amazon/ssm/amazon-ssm-agent.json
```

https://docs.aws.amazon.com/codebuild/latest/userguide/session-manager.html#ssm.prerequisites
