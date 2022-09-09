---
obsidianUIMode: preview
---

```dataviewjs
const filtered_pages = dv.pages('\"700-799 Creative Practices/707 Reading/707.11 Readwise\"').where(p=>p.Tags).where(p=>p.Tags.includes('process') || p.Tags.includes('concept-todo'))
dv.view("rw-inbox-view", filtered_pages);
```