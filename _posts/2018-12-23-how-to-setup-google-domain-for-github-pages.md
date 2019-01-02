---
layout: default
title:  How to setup google domain for github pages
date:   2018-12-23
permalink: /how-to-setup-google-domain-for-github-pages/
cover_url: https://trentyang.com/assets/image/google-domains-and-github-pages/google-domains-and-github-pages-cover.png
comments: true
---

## Intro
Github pages is easy to setup, but to attach a custom domain with google domains, you may run into problems. Here is how you can do it in 4 steps.

## Prerequisites
- You have a [github pages](https://pages.github.com/) repository, e.g. https://github.com/Chun-Yang/Chun-Yang.github.io
- You purchased a domain on [google domain](https://www.domains.google), e.g. trentyang.com

## STEP 1/4: Let gitHub pages know your custom domain
- Go to your github repository settings page
  ![GitHub Settings](https://trentyang.com/assets/image/google-domains-and-github-pages/github-settings.png){:class="zoomable"}

- Add you custom domain name at Settings > GitHub Pages > Custom domain
  ![GitHub Settings Github Pages](https://trentyang.com/assets/image/google-domains-and-github-pages/github-github-pages.png){:class="zoomable"}

## STEP 2/4: Let your custom domain (trentyang.com) points to your github pages
- Go to [registar](https://domains.google.com/m/registrar/) page on your google domains, select your domain
  ![Google Domain Register](https://trentyang.com/assets/image/google-domains-and-github-pages/google-domain-list.png){:class="zoomable"}

- Go to DNS > Custom resource records
  ![DNS Custom resource records](https://trentyang.com/assets/image/google-domains-and-github-pages/google-domain-custom-resource.png){:class="zoomable"}

- Add the record shown in the screenshot bellow. Note that you need to use the "+" button to add more urls.
  ![A record](https://trentyang.com/assets/image/google-domains-and-github-pages/google-domains-a-record.png){:class="zoomable"}
  Here is the list of ips in the screenshot:
  - 185.199.111.153
  - 185.199.110.153
  - 185.199.109.153
  - 185.199.108.153

  
  Incase these are outdated, you can also find the latest ones at [github](https://help.github.com/articles/setting-up-an-apex-domain/#configuring-a-records-with-your-dns-provider).

- To confirm that your DNS record is set up correctly, use the dig command to do a lookup of your domain
  ```console
  $ dig trentyang.com +noall +answer
  trentyang.com.  3600  IN  A  185.199.111.153
  trentyang.com.  3600  IN  A  185.199.110.153
  trentyang.com.  3600  IN  A  185.199.109.153
  trentyang.com.  3600  IN  A  185.199.108.153
  ```

- Once the above is successful, your custom domain should work correctly. Go to your domain and take a look!

## STEP 3/4: Let your www sub-domain (www.trentyang.com) point to your github pages
- Add the following CNAME record
  ![CNAME record](https://trentyang.com/assets/image/google-domains-and-github-pages/cname-record.png){:class="zoomable"}

- You can use the following dig command to confirm that your setup is correct
  ```console
  $ dig www.trentyang.com +nostats +nocomments +nocmd
  www.trentyang.com.      IN      A
  www.trentyang.com. 1263 IN      CNAME   chun-yang.github.io.
  ```

## STEP 4/4: (optional but HIGHLY recommended) Enable HTTPS for your github pages
- Go to your github repository settings page, under Settings > GitHub Pages > Custom domain
  remove your custom domain and save.
  ![GitHub Settings Github Pages](https://trentyang.com/assets/image/google-domains-and-github-pages/github-github-pages.png){:class="zoomable"}
- Then add it back and save again.
- Now you should be able to check the "Enforce HTTPS" checkbox and secure your site!
