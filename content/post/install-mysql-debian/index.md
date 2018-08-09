---
title: "Install MySQL on Debian"
description: "When you can't afford SaaS"
date: "2018-09-09"
tags: ["how-to", "mysql", "debian"]
---

Despite the availability of SaaS solutions like RDS or CloudSQL, it can still be handy to know how to manually install a MySQL server on a Debian machine. Since, to be completely honest, I'm only writing this for future reference, let me just jump right into the details.

```bash
# Check MySQL site for the latest available .deb. Here we download the deb file.
wget https://dev.mysql.com/get/mysql-apt-config_0.8.10-1_all.deb

# Install the deb file
dpkg -i mysql-apt-config_0.8.10-1_all.deb

# Update package lists
apt-get update

# Install MySQL server
apt-get install mysql-community-server
```

And that's it! You're MySQL server should already be running and ready for use! Um, actually, you may still need to configure a user for restricted database access but that can go into another post.
