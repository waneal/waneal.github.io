---
title: "`terraform console` is convenience"
date: 2021-05-28T21:04:16+09:00
draft: false
categories: ["Tech"]
tags: ["Terraform"]
---

I'm using terraform in my company, and I like it. We don't have to memorize all expressions of terraform to use it because of IDE's auto complement function. In addition, sometimes I want to test some expressions quickly. `terraform console` can help it. 

```bash
> terraform console
> [for s in ["a", "b", "c"] : upper(s)]
[
  "A",
  "B",
  "C",
]
```

It is convenience for check values of data and resources because this command can read values in current tfstate.

```bash
> aws_ecr_repository.hoge
{
  "arn" = "arn:aws:ecr:ap-northeast-1:XXXXXXXXXX:repository/hoge"
  "id" = "hoge"
  "image_scanning_configuration" = [
    {
      "scan_on_push" = false
    },
  ]
  "image_tag_mutability" = "MUTABLE"
  "name" = "hoge"
  "registry_id" = "XXXXXXXXXX"
  "repository_url" = "XXXXXXXXXX.dkr.ecr.ap-northeast-1.amazonaws.com/hoge"
  "tags" = {
    "MyTag" = "Hoge"
  }
}

> data.aws_iam_policy.AmazonECSTaskExecutionRolePolicy
{
  "arn" = "arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy"
  "description" = "Provides access to other AWS service resources that are required to run Amazon ECS tasks"
  "id" = "arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy"
  "name" = "AmazonECSTaskExecutionRolePolicy"
  "path" = "/service-role/"
  "policy" = "{...}"
}

https://www.terraform.io/docs/cli/commands/console.html

```