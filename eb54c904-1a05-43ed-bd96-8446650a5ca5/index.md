---
date: 2024-06-26
publish: true
slug: b37ad273-a641-4220-ab43-c098673456fd
tags:
- CS
title: Markdown Parse Survey On Js and Python
uuid: 2962375d-0e26-447b-8605-117d698415db
---
### 目標

取得一份 markdown 的 ast，在遍歷樹結構時同時修改節點值，不會增刪節點，最後在轉換回 markdown
具體專案需求請見 rfmswg
最基本要支援 common markdown，註腳可選

### 結論

只有 [mistune](https://mistune.lepture.com/en/latest/index.html) 可以做到

```python
astrender = MarkdownRenderer()
# plugins=['strikethrough', 'footnotes', 'table','task_lists' , 'math']
ast = mistune.create_markdown(renderer='ast', escape=False)(md)
mdc = astrender(ast, state=mistune.core.BlockState())
```

文件沒有明寫此用法但 v3.0.2 確定可以在專案中使用
plugins 被註解應為加入 plugins 時無法 `astrender` 回 markdown，需要自己撰寫 render

### Survey

背景調查過以下函式庫

- [marked](https://github.com/markedjs/marked) Js 庫
  有 AST 但 AST 只能編譯成 Html，無法編譯回 markdown

- [markdown-it](https://github.com/markdown-it/markdown-it) Js 庫
  文件中找不到 AST 樹資訊

- [remarkable](https://github.com/jonschlinkert/remarkable) Js 庫
  符合 common markdown 的設定會導致 AST 無法編譯回

- [Python-Markdown](https://github.com/Python-Markdown/markdown) Python 庫

  > 我想要解析然後遍歷一個 Markdown 檔案。我正在尋找類似 xml.etree.ElementTree 但適用於 Markdown 的東西
  > 正如另一位評論者提到的，Python-Markdown 具有擴展 API，並且它在內部使用 xml.etree.ElementTree。理論上，你可以創建一個擴展來訪問該內部的 ElementTree 對象，然後對其進行所需的操作。然而，如果你使用原始 HTML（包括 HTML 實體）和/或 codehilite 擴展，則最終獲得的文檔可能是不完整的，因為在序列化的字符串上還有一些後處理器會執行額外的處理。因此，我不太推薦這種方法來達成你的目的。（完整聲明：我是 Python-Markdown 的開發者。）
  > - [Parse and traverse elements from a Markdown file](https://stackoverflow.com/questions/27349951/parse-and-traverse-elements-from-a-markdown-file)



  官方開發者不推薦使用 AST

## [Markdown Parse Implementation List](https://github.com/markdown/markdown.github.com/wiki/Implementations)
