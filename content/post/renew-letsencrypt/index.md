---
title: "Renewing Let's Encrypt Certificate"
description: "Stay secured"
date: "2018-02-22"
tags: ["security", "ssl", "tls", "letsencrypt"]
---

I recently just received an email from [letsencrypt.org](https://letsencrypt.org/) that my SSL certificate was to expire in 20 days. Fearing I may not get another reminder, I decided to renew immediately. Almost automatically, I SSHed into my server. However, I realized I did not actually know how to renew the cert! So I did a little googling and almost immediately found what I was looking for.

> **TLDR;** Run `certbot renew`
>
> Source: https://community.letsencrypt.org/t/renew-letsencrypt-certificate/34677

If you actually came back here then that may mean the command did not exactly run successfully. If so, keep reading. If not, you may still want to keep reading as I'll go over a quick way for you to never have to visit this article again just to renew.

## Fixing 403 Forbidden

So, first the error. In my case, certbot complained of a 403 Forbidden response from my site. The reason for this is was that certbot could not access a hidden directory named `.well-known` to verify my site ownership. To verify whether this is your issue as well, go to your website root e.g. `/var/www/your-project/.well-known` and create a new file.

    # navigate to your site's .well-known directory
    cd /var/www/your-project/.well-known
    # create a file called test.txt
    touch test.txt
    # add a text
    echo "success" > test.txt
    # ensure it is owned by the web server user
    chown www-data:www-data test.txt

Now try to access `yoursite.com/.well-known/test.txt`. If you get a 403 Forbidden, we had the same problem. The webserver does not allow access to the hidden directory `.well-known`. To fix this, you will, intuitively, need to allow/grant access. If you are using nginx as your webserver, you will need to review your site config and look for a section that looks like the following:

    # The following section blocks access to "hidden" files
    # i.e. file names that begin with a dot "."
    location ~ /\. {
        deny                          all;
    }

Under this section, add a directive to allow access to the `.well-known` directory.

    # The following section blocks access to "hidden" files
    # i.e. file names that begin with a dot "."
    location ~ /\. {
        deny                          all;
    }

    # Grant access to allow letsencrypt's certbot to renew certs
    location ^~ /.well-known/ { }

Once edited, you then have to restart your webserver. Depending on your setup, this can be done in a few different ways.

    sudo service nginx restart
    # or
    sudo systemctl restart nginx

Try to access `yoursite.com/.well-known/test.txt` once again to verify you have fixed this issue.

## How to never go through this again

While running a little command like this isn't difficult at all, it would be even better if we never have to do this again. To do this, simply create cron job to regularly run `certbot renew`.

    # Open your crontab
    sudo crontab -e

    # Then add the ff line. This will attempt to renew every first of the month.
    0 0 1 * * certbot renew

Now, you never have to renew your site's SSL cert yourself. Hooray!
