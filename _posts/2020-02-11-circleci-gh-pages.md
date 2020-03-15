---
layout: post
title: "Deploy GH pages using CircleCI"
date: 2020-02-11 16:00:00 +0800
tags: [github-pages, circleCI]
---

- Create Repo
- create branch develop
- follow project on circleCI
- add USER_NAME, USER_EMAIL on circleCI project environment variables
- create deploy key on circleCI with write access. The original one has only read access
- add .circleci/config.yml

locally where was error when adding gem github-pages, trick:

- remove Gemfile.lock, comment off all other gems except github-pages plugin
- run `bundle install`
- uncomment every thing and run `bundle install` again

Reference
https://www.andreagrandi.it/2019/02/24/how-to-deploy-static-website-github-pages-circleci/
https://support.circleci.com/hc/en-us/articles/360018860473-How-to-push-a-commit-back-to-the-same-repository-as-part-of-the-CircleCI-job
https://jtway.co/deploying-jekyll-to-github-pages-with-circleci-2-0-3eb69324bc6e