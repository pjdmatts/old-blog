---
layout: post
title:  "Steps To Blogging With Jekyll"
date:   2015-06-20 19:44:00
categories: jekyll blogging
---

A Recipe for getting started with Jekyll

###Ingredients:###

1, [Jekyll][jekyll]

2, A [Github][github] account


###Instructions###

1, Create a github repository called username.github.io, where
*username* is your user name on GitHub.

2, Find a location where you want to work on your pages and clone
the repository you created in step 1.

```
  $ git clone https://github.com/username/username.github.io
```

3, cd into the username.github.io folder on your machine and create a jekyll site inside that folder.

```
  $ jekyll new .
```

4, Update your local git repository.

```
  $ git commit -am "Initialize Jekyll Site"
```

5, Push the commit back up to the GitHub repository.

```
  $ git push
```

6, Open a browser and take a look at your awesome site at https://username.github.io

7, Your awesome site at https://username.github.io is filled with some
placeholder posts with useful hints on how to get started. You edit and create posts in your sites _posts folder, following the [guide][jekyll-posts] on the [Jekyll][jekyll] website.









[jekyll]:      http://jekyllrb.com
[github]:      https://github.com
[jekyll-posts]: http://jekyllrb.com/docs/posts/
