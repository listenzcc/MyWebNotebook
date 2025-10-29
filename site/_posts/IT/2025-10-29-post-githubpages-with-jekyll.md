---
layout: post
title: "Post Github Pages with Jekyll"
date: 2025-10-29
categories: IT Github Jekyll
---
Details of posting to github pages with jekyll tool.

## Startup

Firstly, follow the [guide][jekyll-docs] to install jekyll.

Secondly, startup the github repository.

Dig into `Settings -> Pages -> Github Actions (Build with jekyll)`
until the `.github\workflows\jekyll-gh-pages.yml` is created.
This project is hosted on [MyWebNotebook.repo][project-repository],
the page is [MyWebNotebook.page][project-page].

Finally, the config.

The `_config.yml` has crucial settings of `baseurl` and `url`,
the pages or assets will be missing if they are not correctly set.
In the project, they are

```yml
# file: _config.yml
baseurl: "/MyWebNotebook" # the subpath of your site, e.g. /blog
url: "https://listenzcc.github.io" # the base hostname & protocol for your site, e.g. http://example.com
```

## Embed HTML & Javascript

Just like embed an image into the post.

<p>
<image src="{{ site.baseurl }}/assets/img/brain.png" height="200" />
</p>

I want to embed `.html` with `.js` scripts too.

<embed type="text/html" src="{{ site.baseurl }}/assets/html/example.html" width="100%" height="200px">

There are 4 issues to be considered.

1. The `<embed ...>` block is good for use.
2. The `src` likes `src="{{ site.baseurl }}/assets/html...`, where the `site.baseurl` locates the correct position of the assets.
3. The `_config.yml` should builds the assets well

    ```yml
    # file: _config.yml
    defaults:
    - scope:
        path: "assets/html"
        values:
        text: true
    - scope:
        path: "assets/src"
        values:
        text: true
    ```

4. The `.html` files find their resources by relative path.
    In the project, I create `html/img/src` subpath under `assets` folder.

    ```html
    <!-- file: html/example.html -->
    <link rel="stylesheet" href="../src/css/basic.css">
    ```

Everything is fine then.

[jekyll-docs]: https://jekyllrb.com/docs/
[project-repository]: https://github.com/listenzcc/MyWebNotebook
[project-page]: https://listenzcc.github.io/MyWebNotebook/
