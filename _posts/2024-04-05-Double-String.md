---
title: "使用Jekyll架網站時，網頁的顯示會出現奇怪的排版。該如何處理?"
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

而且在本機或GitHub上看檔案時，一切都正常，一直到網頁在GitHub Pages上呈現出來後，才看到"走鐘"。

以下提供案例，及處理方式。

# 案例

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

