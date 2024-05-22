---
title: "使用Jekyll架網站時，GitHub Pages網頁的顯示會出現奇怪的排版。該如何處理?"
date: 2024-05-22 10:21:00 +0800
excerpt: ""
categories: 
  - GitHub Pages
tags:
  - Solving issues
  - 問題處理
  - Jekyll
  - Markdown
toc: true
toc_sticky: false
toc_label: "Table of contents"
toc_icon: "columns"
---

有時候，使用Jekyll架網站時，網頁的顯示會出現奇怪的排版。

而且有時候，在本機或GitHub上看檔案時，一切都正常，一直到網頁在GitHub Pages上呈現出來後，才看到"走鐘"。

以下提供案例，及處理方式。

# 案例1

## 狀況

Markdwon的檔案寫這樣:

```markdown
YouTube: [B. B. King - The Thrill Is Gone (Live at Montreux 1993) | Stages](<https://www.youtube.com/watch?v=4fk2prKnYnI>)
```

結果顯示成這樣:

YouTube: [B. B. King - The Thrill Is Gone (Live at Montreux 1993) | Stages](<https://www.youtube.com/watch?v=4fk2prKnYnI>)

NOTE: 在本機或GitHub上看檔案時，一切都正常，一直到網頁在GitHub Pages上呈現出來後，才看到"走鐘"。

## 處理方式

將Markdwon的檔案改寫，在`|`前面加入`\`。

```markdown
YouTube: [B. B. King - The Thrill Is Gone (Live at Montreux 1993) \| Stages](<https://www.youtube.com/watch?v=4fk2prKnYnI>)
```

顯示就變正常了:

YouTube: [B. B. King - The Thrill Is Gone (Live at Montreux 1993) \| Stages](<https://www.youtube.com/watch?v=4fk2prKnYnI>)

NOTE: 在`|`前面加入`\`後，在本機或GitHub上看檔案時，也仍保持正常。

# 案例2

## 狀況

Markdwon的檔案寫這樣:

```markdown
title: "使用Jekyll架網站時，"GitHub Pages"網頁的顯示會出現奇怪的排版。該如何處理?"
```

在GitHub Pages文字的左邊跟右邊都加上`"`，結果就是造成title消失。

## 處理方式

將Markdwon的檔案改寫，在`"`前面加入`\`。

```markdown
title: "使用Jekyll架網站時，\"GitHub Pages\"網頁的顯示會出現奇怪的排版。該如何處理?"
```

顯示就變正常了。
