---
title: "Speed Testing a DNS"
description: "Dig this"
date: "2018-10-07"
tags: ["dns", "performance", "dig", "internet-connection"]
---

It can sometimes be useful to check your DNS's performance. I have found that on some occasions the DNS causes a perceivably slow internet access and switching from one to another resulted in a delightfully faster connection. A couple months ago, I learned simple way to speed test a DNS server. It's not a long or complex command but can be easy to forget when you only use it once in a while.

```bash
dig @x.x.x.x example.com | grep "Query time"
```

My DNSs of choice are usually just Google and Cloudflare because their server IPs are so easy to remember. When one is slow, I usually just switch to the other.

| DNS        | Primary IP | Secondary IP |
| ---------- | ---------- | ------------ |
| Google     | 8.8.8.8    | 8.8.4.4      |
| Cloudflare | 1.1.1.1    | 1.0.0.1      |

To check whether switching DNS can remedy a slow internet access, simply test the DNS.

```bash
dig @1.1.1.1 example.com | grep "Query time"
;; Query time: 33 msec

dig @8.8.8.8 example.com | grep "Query time"
;; Query time: 46 msec
```

At the time of writing, internet access was pretty fast so in that case it can still be nice to know which DNS would be optimal to use based on query time. 
