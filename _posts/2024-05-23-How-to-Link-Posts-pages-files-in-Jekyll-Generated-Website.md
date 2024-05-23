---
title: "在使用Jekyll建置的網頁中，該如何在Markdown檔案中，連結站內資源。例如: post, page, collection item, file等。"
date: 2024-05-23 00:30:00 +0800
excerpt: ""
categories:
  - GitHub Pages
tags:
  - Jekyll
  - Liquid
  - Markdown
toc: true
toc_sticky: false
toc_label: "Table of contents"
toc_icon: "columns"
---

在使用Jekyll建置的網頁中，該如何在Markdown檔案中，連結站內資源。例如: post, page, collection item, file等。

# 1. 結論

在Markdown檔案中使用Liquid語法

可使用
```markdown
[Link to a post section]({{ site.baseurl }}{% link _posts/2024-05-23-Test-Post-01.md %}#section-2)
```

效果:  
[Link to a post section]({{ site.baseurl }}{% link _posts/2024-05-23-Test-Post-01.md %}#section-2)

NOTE: 如果不要連結到章節，請刪除`#section-2`。

優點: 使用這個語法的好處是，不管在本機或者GitHub Page上，都可以順利連結到該post。這樣對於喜歡先在本機進行post預覽的人而言，很方便。只要本機預覽OK，那post上傳到GitHub後，GitHub Page的顯示也OK。

# 2. 尋找解決方案

Jekyll官方文件有說明。

REF:  
Jekyll: [Tags Filters/#links](https://jekyllrb.com/docs/liquid/tags/#links)

## 2.1 Linking to pages

可使用`link` tag來產生permalink URL。這樣有一個好處，如果permalink style改變了，那這個`link` tag仍然有效，讓網頁仍然可以連到。

使用`link` tag的連結會長這樣:

{% raw %}
```liquid
{% link _posts/2024-05-24-name-of-post.md %}
{% link news/index.html %}
{% link /assets/files/document.pdf %}
{% link _collection/name-of-document.md %}
```
{% endraw %}

也可使用`link` tag在Markdown的語法中，像這樣:

{% raw %}
```markdown
[Link to a post]({% link _posts/2024-05-24-name-of-post.md %})
[Link to a page]({% link news/index.html %})
[Link to a file]({% link /assets/files/document.pdf %})
[Link to a collection]({% link _collection/name-of-document.md %})
```
{% endraw %}

這個`link` tag是建造一個相對於跟目錄(`/`)的路徑。

使用`link` tag有個好處，就是驗證連結。當連結不存在時，Jekyll不會build站點。這樣會提醒架站者去修正問題。

可能會看到的Error message長這樣
```
Liquid Exception: Could not find document '_posts/[name-of-post].md' in tag 'link'. 
Make sure the document exists and the path is correct. 
in D:/Jekyll/[name-of-site]/_posts/[name-of-post].md
```

## 2.2 Linking to posts

使用`post_url` tag可以產生post的permalink URL。

{% raw %}
```liquid
{% post_url 2024-07-21-name-of-post %}
```
{% endraw %}

如果post是放在`/_posts`的子目錄下面，假設該子目錄名稱為`subfolder`

{% raw %}
```liquid
{% post_url /subfolder/2024-07-21-name-of-post %}
```
{% endraw %}

在Markdown檔案中，製作連結的方式就變為

{% raw %}
```markdown
[Name of Link]({% post_url 2024-07-21-name-of-post %})
```
{% endraw %}

NOTE: 使用`post_url`這個方式，就不用加上副檔名。例如`2024-07-21-name-of-post.md`的`.md`可去掉。

NOTE: `post_url`與`link`這兩個方式相比較，使用`post_url`可省略打上`_posts/`跟副檔名(例如: `.md`)。

NOTE: 沒辦法使用Liquid filter，{% raw %}`{% link mypage.html | append: "#section1" %}`{% endraw %}去連結到章節。

# 3. 使用案例

## 3.1 連結站內的post

Markdown語法:
{% raw %}
```markdown
[Link to a post]({{ site.baseurl }}{% link _posts/2024-05-23-Test-Post-01.md %})
```
{% endraw %}

效果:
[Link to a post]({{ site.baseurl }}{% link _posts/2024-05-23-Test-Post-01.md %})

## 3.2 連結站內的post的章節

假設要連到站內某個post下面的章節。  
例如: `2024-05-23-Test-Post-01.md`這個post下面有三個section。

### 3.2.1 方法1

可使用
```markdown
[Link to a post section]({{ site.url }}{{ site.baseurl }}/2024/05/23/Test-Post-01/#section-1)
```

效果:  
[Link to a post section]({{ site.url }}{{ site.baseurl }}/2024/05/23/Test-Post-01/#section-1)

### 3.2.2 方法2

也可使用
```markdown
[Link to a post section]({{ site.baseurl }}{% link _posts/2024-05-23-Test-Post-01.md %}#section-1)
```

效果:  
[Link to a post section]({{ site.baseurl }}{% link _posts/2024-05-23-Test-Post-01.md %}#section-1)

### 3.2.3 不行的方法

沒辦法使用Liquid filter去連結到章節。
{% raw %}
```liquid
{% link mypage.html | append: "#section1" %}
```
{% endraw %}

NOTE: 

經過測試，把下面這行，硬寫上Markdown檔案裡面。在Jekyll進行build動作時，就會發生error，停止build。

{% raw %}
```markdown
[Section of Link]({% link _posts/2024-05-23-Test-Post-01.md | append: "#section-1" %})
```
{% endraw %}

## 3.3 連結站內的檔案

Markdown語法:
{% raw %}
```markdown
[Link to a figure file]({{ site.baseurl }}{% link /assets/images/2024/This-is-a-Figure-1920px-1080px.jpg %})
```
{% endraw %}

[Link to a figure file]({{ site.baseurl }}{% link /assets/images/2024/This-is-a-Figure-1920px-1080px.jpg %})

# 4. 延伸使用

## 4.1 顯示站內圖檔

Markdown語法:
{% raw %}
```markdown
![Link to a figure]({{ site.baseurl }}{% link /assets/images/2024/This-is-a-Figure-1920px-1080px.jpg %})
```
{% endraw %}

效果:
![Link to a figure]({{ site.baseurl }}{% link /assets/images/2024/This-is-a-Figure-1920px-1080px.jpg %})


# 5. 感想

1. Jekyll有很多好用的工具，方便架站者使用。
2. 看起來，又要對網站連結大改版了。

# 6. 相關Po文









# 7. 相關連結

Jekyll: [Tags Filters/#links](https://jekyllrb.com/docs/liquid/tags/#links)
<!--
Jekyll (GitHub): [docs/_docs/liquid/tags.md](https://github.com/jekyll/jekyll/blob/master/docs/_docs/liquid/tags.md)
-->

Stack overflow: [jekyll markdown internal links](https://stackoverflow.com/questions/4629675/jekyll-markdown-internal-links)

Jekyll: [Permalinks](https://jekyllrb.com/docs/permalinks/)
