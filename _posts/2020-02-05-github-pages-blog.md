---
layout: post
title: "Blog with Githut Pages"
date: 2020-02-05 09:00:00 +0800
tags: [github-pages]
---

For a long time I have been wanting to setup a personal blog where things can get organized and customized at the same time.
However it was just too time consuming, with all the DB setup, servers, deployment, etc.

## Githut pages + Jekyll

**A blog with PURE content**

I discovered [Githut pages](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site), and found it simple enough and yet flexible in terms of styles.
Once setup, it allows you to focus purely on the content which is Markdown, also it's possible to write in offline mode. Publishing content is as easy as "git commit && git push"

Thanks to [blog post by Arya Murali](https://medium.com/20percentwork/creating-your-blog-for-free-using-jekyll-github-pages-dba37272730a)


**Setup in 4 step**

1. setup a repo for the blog site
   `https://github.com/<github_username>/<repo_name>`
2. source for a [Jekyll theme](https://jekyllrb.com/docs/themes/) of your choice
3. clone the repo locally, cd into it, git init, customize it and commit locally
4. publish the site from branch gh-pages (default name to allow github pages build your site automatically)

```bash
# create a local branch gh-pages
git checkout -b gh-pages
git remote add origin <repo_url_in_step_1>
git remote -v # verification of remote

# push gh-pages into remote repo
git push origin gh-pages
```

If done correctly, the site will be available at
`https://<github_username>.github.io/<repo_name>/`

After step 3, to test the site locally @ http://127.0.0.1:4000/, run:

```bash
bundle install
bundle exec jekyll build
bundle exec jekyll serve
```
