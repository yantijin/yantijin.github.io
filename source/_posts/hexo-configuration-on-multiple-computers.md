---
title: hexo configuration on multiple computers
date: 2018-11-04 10:47:42
tags: Try4New
categories: Entertainment
mathjax: false
---

### Todo for myself

* Install [node.js](https://nodejs.org/en/)

* Install hexo

  ```shell
  npm  install -g hexo
  ```

* Download latest version in my Gituhb

  ```shell
  git clone https://github.com/yantijin/yantijin.github.io.git
  ```

* Download latest themes configuration in another foler

  ```
  git clone https://github.com/yantijin/Theme_Next.git
  ```

  Then copy the theme into **github.yantijin.io/themes**

* Install  dependencies for your blog

  ```shell
  npm install
  ```

* Something needs to modifiy

  * About **MATHJAX**

    ```shell
    npm uninstall hexo-readerer-marked --save
    npm install hexo-renderer-kramed --save
    ```

     Next step is to modify the files in **node_modules/kramed/lib/rules/inlime.js**.

    Change line 10 and line 20:

    ```javascript
    // escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,
    escape: /^\\([`*\[\]()#$+\-.!_>])/,
    // em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
     em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
    ```

    ​

* [REF for Detail](https://juejin.im/post/5acf22e6f265da23994eeac9)

