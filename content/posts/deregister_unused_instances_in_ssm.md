---
title: "Deregister unused instances in SSM"
date: 2021-05-12T21:29:35+09:00
draft: false
categories: ["Tech"]
tags: ["AWS", "SSM"]
---

AWS Systems Manager can manage instances by Fleet Manager. It can cover not only aws instances, but also on-premiss instances by Hybrid Activations. For example, using Hybrid Activations and managing servers which are under control of auto-scaling function in on-premiss environment, some servers become `ConnectionLost` status in Fleet Manager when their servers are terminated by scale in action. At result, unused servers continue existing in Fleet Manager.

To resolve that problem, I regularly clean up unused instances by below lambda function.

```python

import logging

import boto3

logger = logging.getLogger()
logger.setLevel(logging.INFO)

client = boto3.client('ssm')
paginator = client.get_paginator('describe_instance_information')


def deregister_unused_instances():
    for page in paginator.paginate():
        for instance in page['InstanceInformationList']:
            if instance['PingStatus'] != 'Online':
                logger.info(f"deregister instance: {instance['InstanceId']}")
                client.deregister_managed_instance(InstanceId=instance['InstanceId'])
    return 0


def lambda_handler(event, context):
    deregister_unused_instances()

```