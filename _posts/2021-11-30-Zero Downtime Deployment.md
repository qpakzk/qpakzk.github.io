---
layout: post
title: "Zero Downtime Deployment: A Comparative Analysis of Methodologies"
description: ""
tags: [DevOps]
redirect_from:
  - /2021/11/30/
---

# Zero Downtime Deployment: A Comparative Analysis of Methodologies

The software deployment landscape has evolved, necessitating methodologies that prevent service interruptions. In the modern era of continuous deployment[^1], achieving zero downtime during deployments has become paramount. This article elucidates three predominant techniques for achieving this feat: Rolling Deployment, Blue-Green Deployment, and Canary Deployment. All these methodologies harness the capabilities of load balancers to maintain service continuity.

## Rolling Deployment

This approach entails deploying the new version sequentially across application instances. It negates the need for additional infrastructure, thereby being cost-efficient. 

While resource-effective, the challenge lies in ensuring compatibility between the concurrently running versions. If the versions are not backward-compatible, inconsistencies may arise, potentially compromising the system's integrity.

## Blue-Green Deployment

This method involves maintaining two parallel environments for the application. Upon deploying the new version on the secondary environment, traffic is rerouted to it.

Though this method offers a rapid rollback mechanism, it necessitates duplicating resources. While the switch between environments is seamless, any disparity in data between the two might result in complications.

## Canary Deployment

Canary Deployment is characterized by deploying the new version to a limited set of instances, gradually increasing its exposure based on feedback and performance metrics.

While allowing for real-time feedback, a crucial consideration is the representativeness of the selected user subset. Any misrepresentation can lead to overlooking potential system-wide issues.

## Conclusion

In an era where continuous deployment has become the norm, the significance of zero downtime deployment methodologies cannot be understated. Each technique discussed presents unique advantages and challenges. The onus lies on organizations to critically evaluate these based on their infrastructure, risk appetite, and deployment cadence.

## Bibliography

- [Samsung SDS](https://www.samsungsds.com/kr/insights/1256264_4627.html)
- [Potato Yong's Blog](https://potato-yong.tistory.com/136)
- [Harness](https://harness.io/blog/blue-green-canary-deployment-strategies/)
- [Cloudbees Blog on Rolling Deployment](https://www.cloudbees.com/blog/rolling-deployment)
- [Cloudbees Blog on Blue-Green Deployment](https://www.cloudbees.com/blog/blue-green-deployment)


[^1]: Continuous Deployment Trends, [Link](https://imgur.com/a/3uBZKBN)
