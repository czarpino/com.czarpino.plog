---
title: "Storing Database Backups"
description: "Nope, not easy too"
date: "2018-04-07"
tags: ["backup", "database"]
---

Where to store database backups has been a long recurring conversation in most teams I've worked with. This comes as no surprise as it is undoubtedly necessary to backup data. Data loss is a serious risk and any server admin worth his salt takes backing up seriously.

The short version of the advice I often give is to use [S3](https://aws.amazon.com/s3/) or an S3-like service (e.g. [Glacier](https://aws.amazon.com/glacier/), [Archival](https://cloud.google.com/storage/archival/)). The reason being, these services promise the two most important factors of a backup storage: durability and security.

## Storage must be durable

Since a backup is typically a worst-case fallback, the storage medium must be very durable. This means, the storage itself must be highly resistant to data loss. The last thing you want is a corrupted backup when trying to recover lost data.

Storage concerns regarding durability are important because there are typically no recovery mechanisms for lost backups. It is therefore important to focus on preventative measures to ensure there is zero data loss in backup data. This means accounting for hardware failure, human error, and natural data degradation.

## Storage must be secure

Another important characteristic of a good backup storage is security. This is pretty intuitive considering backups typically contain sensitive data of both the business and it's customers. It is, therefore, important to ensure data is encrypted during transit and at rest: this means using TLS and storage encryption. An intermediate node in the network and someone with physical access to the backup's machine should both be unable to view the data in plain text.

## Convenience and reliability

Ensuring the durability and security of backup storage requires significant effort. The second reason for recommending S3-like services, which closely follows the first, is convenience and reliability. Services like S3 already have solid infrastructures in place which address durability and security concerns. Extensively documented SDKs for programmatically interfacing with the service are also provided. These conveniences are possible largely because storage and retrieval of data is the core of their business.

While it is entirely possible to build your own durable and secure storage server, it will not be without significant effort. Achieving a level of reliability 3rd party services provide will require resources better spent building your actual product.

Using a regular server instance and configuring it yourself is a common and naive recommendation. Unfortunately, it is not only inferior in every aspect but is also more expensive. Utilizing S3 or a similar service is the most prudent choice unless you have an unusually special situation.

## Summary

There are a few key considerations for a reliable backup storage including durability and security. Trying to achieve this yourself can easily side track you from the core operations of your business while still ending up with an inferior storage solution. The most prudent way to store backups is by employing specialized and reputable services such as Amazon S3, Glacier, or Google Archival. All excellent choices considering the convenience and reliability they have over building your own.
