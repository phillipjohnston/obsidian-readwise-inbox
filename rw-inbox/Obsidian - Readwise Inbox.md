==where I got==
I can properly access the target tag…
now I need to 

https://github.com/TfTHacker/obsidian-readwise-inbox

What I would like:
- ability to change tags in my readwise inbox, without the website (could probably build an Alfred key around this)

https://readwise.io/api_deets

## Tagging API

## Highlight Tag CREATE

**Request**: `POST` to `https://readwise.io/api/v2/highlights/<highlight id>/tags/`

**Parameters:** A JSON object with the following key:

Key

Type

Description

Required

name

string

The tag's name.

yes

**Response:**

-   Status code: `200`
-   Highlight's tag:

```

{
  "id": 11311390,
  "name": "philosophy"
}
              
```

**Usage/Examples:**

-   JavaScript

```

$.ajax({
  url: 'https://readwise.io/api/v2/highlights/59767830/tags',
  type: 'POST',
  contentType: 'application/json',
  beforeSend: function (xhr) {
    xhr.setRequestHeader('Authorization', 'Token XXX');
  },
  data: JSON.stringify({
    "name": "philosophy",
  }),
  success: function (result) {
    console.log(result)
  },
  error: function (error) {
    console.log(error)
  },
});
          
```

-   Python

```

import requests

requests.post(
    url="https://readwise.io/api/v2/highlights/59767830/tags",
    headers={"Authorization": "Token XXX"},
    json={"name": "philosophy"}
)

data = response.json()
                    
```

## Highlight Tag UPDATE

**Request**: `PATCH` to `https://readwise.io/api/v2/highlights/<highlight id>/tags/<tag id>`

**Parameters:** A JSON object with the following key:

Key

Type

Description

Required

name

string

The tag's name.

yes

**Response:**

-   Status code: `200`
-   Updated highlight's tag:

```

{
  "id": 11311390,
  "name": "continental philosophy"
}
              
```

**Usage/Examples:**

-   JavaScript

```

$.ajax({
  url: 'https://readwise.io/api/v2/highlights/59767830/tags/11311390',
  type: 'PATCH',
  contentType: 'application/json',
  beforeSend: function (xhr) {
    xhr.setRequestHeader('Authorization', 'Token XXX');
  },
  data: JSON.stringify({
    "name": "continental philosophy",
  }),
  success: function (result) {
    console.log(result)
  },
  error: function (error) {
    console.log(error)
  },
});
          
```

-   Python

```

import requests

requests.patch(
    url="https://readwise.io/api/v2/highlights/59767830/tags/11311390",
    headers={"Authorization": "Token XXX"},
    json={"name": "continental philosophy"}
)

data = response.json()
                    
```

## Highlight Tag DELETE

**Request**: `DELETE` to `https://readwise.io/api/v2/highlights/<highlight id>/tags/<tag id>`

**Parameters:**  
This endpoint doesn't take any parameters.

**Response:**

-   Status code: `204`

**Usage/Examples:**

-   JavaScript

```

$.ajax({
  url: 'https://readwise.io/api/v2/highlights/59767830/tags/11311390',
  type: 'DELETE',
  contentType: 'application/json',
  beforeSend: function (xhr) {
    xhr.setRequestHeader('Authorization', 'Token XXX');
  },
  success: function (result) {
    console.log(result)
  },
  error: function (error) {
    console.log(error)
  },
});
          
```

-   Python

```

import requests

response = requests.delete(
    url="https://readwise.io/api/v2/highlights/59767830/tags/11311390",
    headers={"Authorization": "Token XXX"},
```

## Old Export
- {{ highlight_text }}{% if highlight_location and highlight_location_url %}
    - [{{highlight_location}}]({{highlight_location_url}}){% elif highlight_location %} ({{highlight_location}}){% endif %}{% if highlight_tags %}
    - Tags: {% for tag in highlight_tags %}[[{{tag}}]] {% endfor %}{% endif %}{% if highlight_note %}
    - Note: {{ highlight_note }}{% endif %}

## New Export

- {{ highlight_text }} ^rw{{highlight_id}}
    - {% if highlight_location and highlight_location_url %}[{{highlight_location}}]({{highlight_location_url}}), {% elif highlight_location %} {{highlight_location}}, {% endif %}[Open in Readwise](https://readwise.io/open/{{highlight_id}}){% if highlight_tags %}
    - Tags: {% for tag in highlight_tags %}[[{{tag}}]] {% endfor %}{% endif %}{% if highlight_note %}
    - Note: {{ highlight_note }}{% endif %}

---

## His README

The Readwise Inbox tool provides an inbox of highlights that need to be processed. Processing depends on your workflow, but mine works like this:

-   Highlights are imported via the [Readwise plugin](https://github.com/readwiseio/obsidian-readwise). I never edit the files imported by Readwise directly. This way if my highlights are exported, my personal notes linked to them are never broken.
-   In another note that I create in my vault, I make notes on the imported highlights. I do not edit the export file. If I want to refer to contents of a highlight, I block reference it. For more info on block references, see this link to [Links to Block](https://help.obsidian.md/How+to/Link+to+blocks) in the Obsidian online help.
-   Once I have made my note, I mark the highlight has processed in the Readwise Inbox by clicking on the button with the X in it.

With this tool, you can see an "inbox" of unproccessed highlights from readwise. You process each highlight one at a time. If you click X button, it marks it as complete and disappears from your inbox.

You can use the A and T buttons to copy block references to your clipboard. These references are then used in your own personal notes to refer back to the block reference.

## [](https://github.com/TfTHacker/obsidian-readwise-inbox#additional-features)Additional features

The tool has 3 buttons for each highlight. The following list describes the button

-   X - Marks the highlight as processed
-   B - Copies a block reference to the clipboard
-   A - Copies a block reference as an alias with an asterisk to the clipboard
-   T - Copies the text of the higlight and a block reference as an alias with an asterisk to the clipboard

The + sign at the end is a link to the block reference in the file.

## [](https://github.com/TfTHacker/obsidian-readwise-inbox#additional-information)Additional information

This tool builds on the concept presented in this article [Using Readwise’s highlight_id as a single source of truth in Obsidian](https://tfthacker.medium.com/using-readwises-highlight-id-as-a-single-source-of-truth-in-obsidian-b1de98a8b87c).

This tool assumes that each highlight has an assigned block identifier based on the Readwise highlight identifier.

# [](https://github.com/TfTHacker/obsidian-readwise-inbox#dependencies)Dependencies

The following Obsidian plugins are required for this solution:

-   Plugin: Readwise Official Plugin
    -   It is assumed this plugin is configured and the highlights are synced into your vault.
    -   also that you have enabled a unique block identifier for each highlight as mentioned in the "Additional information" section of this readme file.
-   Plugin: Dataview
    -   In settings, **Enable JavaScript Queries** needs to be toggled on
-   Plugin: Buttons

# [](https://github.com/TfTHacker/obsidian-readwise-inbox#installation)Installation

Copy the rw-inbox folder (and all its contents) into your vault.

With this folder in your vault, open the rw-inbox-viewer.md file. This will display your highlights from the Readwise export folder.

This folder consists of the following:

-   subfolder called **rw-inbox-view**. The files in this folder should not be edited. It is the code used by the Dataview plugin to create the view of our readwise inbox.
-   file **rw-inbox-config.md** contains the default configuration information for this solution
-   file **rw-inbox-log-processed.md** contains the log of processed highlights. Normally you would not edit this file. It contains the block reference id numbers of processed highlights.
-   file **rw-inbox-viewer.md** is an example of how to use this solution. It contains a dataviewjs query that can be used in any markdown file in your vault. See the next section for more details.

# [](https://github.com/TfTHacker/obsidian-readwise-inbox#how-to-use)How to use

A simple dataviewjs query formatted as follows will retrieve your Readwise highlights:

````
```dataviewjs
dv.view("rw-inbox-view");
```
````

This dataviewjs query can be put into any page.

You can control some aspects of the output of this query by using the following [front matter](https://help.obsidian.md/Advanced+topics/YAML+front+matter):

-   LimitHighlightCount - number of highlights to display
-   SortDateAscending - default sort is date ascending. Set to false for it to sort in descending date order.

# [](https://github.com/TfTHacker/obsidian-readwise-inbox#querying-for-specific-information)Querying for specific information

The rw-inbox-view accepts an optional parameter, a dv.pages object. This object can be used to provide a refined set of pages based on a JavaScript Dataview query.

The following example return just tweets:

````
```dataviewjs
const tweets = dv.pages('"Readwise/tweets"')
dv.view("rw-inbox-view", tweets );
```
````

All Twitter highlights from this year:

````
```dataviewjs
const tweets = dv.pages('"Readwise/tweets"').filter(p=>new Date(p.created)>new Date("2022-01-01"))
dv.view("rw-inbox-view", tweets );
```
````

Highlights that have been tagged with #priority, and from the readwise export folder

````
```dataviewjs
const byTags = dv.pages("#priority and \"30-Files/99-ReadwiseSync\"")
dv.view("rw-inbox-view", byTags );
```
````

Highlights that have been tagged with #priority or #important, and from the readwise export folder

````
```dataviewjs
const byTags = dv.pages("(#priority or #important) and \"30-Files/99-ReadwiseSync\"")
dv.view("rw-inbox-view", byTags );
```
````

Return all highlights with the frontmatter source value equal to a specific author

````
```dataviewjs
const byAuthor = dv.pages('"30-Files/99-ReadwiseSync"').where(p=>p.file.frontmatter?.author=='nickwignall.com')
dv.view("rw-inbox-view", byAuthor);
```
````