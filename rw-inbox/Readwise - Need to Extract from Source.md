---
FilterTags: extract
OnProcessRemoveTags: extract
---

```dataviewjs
const filtered_pages = dv.pages("#extract and \"700-799 Creative Practices/707 Reading/707.11 Readwise\"");
dv.view("rw-inbox-view", filtered_pages);
```
