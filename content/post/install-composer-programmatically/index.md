---
title: "Installing Composer Programmatically"
description: "Let's get this one right"
date: "2018-10-14"
tags: ["php", "bash", "dependency-management"]
---

I have found it quite concerning that people usually setup up a programmatic Composer installation incorrectly. I feel since Composer's download page describes the download process using a script, people take it as the programmatic way of installing. This is, of course, an incorrect assumption which can be inferred from the hard coded installer SHA used in the sample script.

After recently dealing with build failures caused by an outdated installer hash, I wanted to address this issue correctly instead of simply kicking it down the road.

### Updating the installer hash

Before talking about the proper solution, I want to highlight the improper but quick solution: updating the installer hash. If you urgently need to get something done and want to address the installer issue separately, it is helpful in the short term to simply update the installer SHA hash.

```bash
# Replace "93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8"
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

If you visit [Composer's download page](https://getcomposer.org/download/), you will quickly see the latest hash in the sample script. Alternatively, you can also check via the command line:

```bash
# via wget
wget -q -O - https://composer.github.io/installer.sig

# or via cURL
curl https://composer.github.io/installer.sig
```

### Programmatic installation

The proper way to programmatically install Composer is to _not_ rely on a hard coded hash. Looking a little closer, Composer download documentation actually links to the [programmatic way of installing](https://getcomposer.org/doc/faqs/how-to-install-composer-programmatically.md). 

```bash
#!/bin/sh

EXPECTED_SIGNATURE="$(wget -q -O - https://composer.github.io/installer.sig)"
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
ACTUAL_SIGNATURE="$(php -r "echo hash_file('SHA384', 'composer-setup.php');")"

if [ "$EXPECTED_SIGNATURE" != "$ACTUAL_SIGNATURE" ]
then
    >&2 echo 'ERROR: Invalid installer signature'
    rm composer-setup.php
    exit 1
fi

php composer-setup.php --quiet
RESULT=$?
rm composer-setup.php
exit $RESULT
```

This script downloads the installer, verifies the hashes, then installs Composer. It checks the installer SHA against the latest hash obtained from https://composer.github.io/installer.sig whose value is automatically updated when a new release is made. This way, no hard coded hash is used within the script and you automatically get the latest version of Composer.

You have now future proofed programmatic Composer installation!
