---
layout: post
title:  How to setup google domain for github pages
date:   2018-12-23
permalink: /how-to-setup-google-domain-for-github-pages/
categories: hosting
---
## Intro
Github pages is easy to setup, but to attach a custom domain with google domains, you may run into problems. Here are how you can do it in 3 steps.

## Prerequisites
- You have a [github pages](https://pages.github.com/) repository, e.g. https://github.com/Chun-Yang/Chun-Yang.github.io
- You purchased a domain on [google domain](https://www.domains.google), e.g. charlieyankeeblog.com

## STEP 1/3: Add your custom domain to your GitHub Pages site
- Go to your github repository settings page
  ![GitHub Settings](/assets/image/google-domains-and-github-pages/github-settings.png)

- Add you custom domain name at Settings > GitHub Pages > Custom domain
  ![GitHub Settings Github Pages](/assets/image/google-domains-and-github-pages/github-github-pages.png)

## STEP 2/3: Configure "A records" with google domains
- Go to [registar](https://domains.google.com/m/registrar/) page on your google domains, select your domain
  ![Google Domain Register](/assets/image/google-domains-and-github-pages/google-domain-list.png)

- Go to DNS > Custom resource records
  ![DNS Custom resource records](/assets/image/google-domains-and-github-pages/google-domain-custom-resource.png)

- Add the record shown in the screenshot. Note that you need to use the "+" button to add more urls.
  ![A record](/assets/image/google-domains-and-github-pages/google-domains-a-record.png)
  Here is the list of ips in the screenshot. Incase they are outdated, you can find it at [github](https://help.github.com/articles/setting-up-an-apex-domain/#configuring-a-records-with-your-dns-provider).
  - 185.199.111.153
  - 185.199.110.153
  - 185.199.109.153
  - 185.199.108.153

- To confirm that your DNS record is set up correctly, use the dig command to do a lookup of your domain
  ```
  $ dig +noall +answer charlieyankeeblog.com
  charlieyankeeblog.com.  3600  IN  A  185.199.111.153
  charlieyankeeblog.com.  3600  IN  A  185.199.110.153
  charlieyankeeblog.com.  3600  IN  A  185.199.109.153
  charlieyankeeblog.com.  3600  IN  A  185.199.108.153
  ```

- Once the above is successful, your custom domain should work correctly. Go to your domain and take a look!

## STEP 3/3: (optional but HIGHLY recommended) Enable https for your github pages
- Go to your github repository settings page,
  remove and add your custom domain name back under the Settings > GitHub Pages > Custom domain
  ![GitHub Settings Github Pages](/assets/image/google-domains-and-github-pages/github-github-pages.png)
- Now you should be able to check the "Enforce HTTPS" checkbox and secure your site!
