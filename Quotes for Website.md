---
obsidianUIMode: preview
FilterTags: [ea-website]
FilterTagsToExclude: [ea-website-used]
OnProcessRemoveTags: [ea-website, concept-todo]
OnProcessAddTags: [ea-website-used, concept-processed]
FilterFromClipboardCopy: '{Tagged: .*}'
---

```dataviewjs
const AnkiTodoQuotes = dv.pages("#ea-website and \"700-799 Creative Practices/707 Reading/707.11 Readwise\"");
dv.view("rw-inbox-view", AnkiTodoQuotes);
```
