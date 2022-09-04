---
FilterTags: todo
FilterTagsToExclude: ['concept-todo', 'anki-todo']
OnProcessRemoveTags: todo
OnProcessAddTags: todo/processed
---

```dataviewjs
const filtered_pages = dv.pages("#todo and \"700-799 Creative Practices/707 Reading/707.11 Readwise\"");
dv.view("rw-inbox-view", filtered_pages);
```
