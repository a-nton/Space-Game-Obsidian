## Markdown Basics

*Markdown is inline annotation. The formatting lives inside the text as characters, and when rendered, those characters disappear and their effect takes their place. You're writing the instructions for how the text should look directly into the text itself.

Formatting is invisible until you click on something to edit it*

**Headings** — number of `#` sets the level:

```
# Heading 1
## Heading 2
### Heading 3
```

**Bold** and _italic_:

```
**bold**
*italic*
***bold italic***
```

**Links** in Obsidian:

```
[[File Name]]
[[File Name#Heading]]
[[File Name|display text]]
```

**External links:**

```
[display text](https://example.com)
```

**Lists. Two types:**

```
- item
- item
  - nested item

1. numbered
2. numbered
```

**Checkboxes:**

```
- [ ] undone
- [x] done
```

**Images** (from your vault):

```
![[image-name.png]]
```

**Blockquotes:**

```
> quoted text
```

**Code** — inline with single backticks, blocks with triple. The gray boxes you see in this section are also formatted thus:

````
Inline: `some code`

Block:
```
multiple lines
of code
```
````

**Horizontal rule:**

```
---
```

**Tables:**

```
| Column A | Column B |
|----------|----------|
| cell     | cell     |
| cell     | cell     |
```

**Tags:**

```
#tagname
```

**Strikethrough:**

```
~~crossed out~~
```

**Footnotes:**

```
Some claim[^1] deserves a note.

[^1]: The note text goes here.
```

That covers everything you'd use day to day. The only Obsidian-specific things are `[[wikilinks]]` and `![[embeds]]` — standard markdown uses `[text](url)` for links instead.


## Other Functionality
### **How to insert links?**

Type `[[` and Obsidian will autocomplete from existing file names. So `[[The Beholder` will pop up a suggestion for `The-Beholder.md`. You can also link to a specific heading within a file with `[[The-Beholder#Design Notes]]`, and you can rename how the link displays with `[[The-Beholder|the entity in the void]]`.
	
### **How to add tags?**

Just type `#tagname` anywhere in a note. No setup needed. The tags I defined in the Conventions file (`#unresolved`, `#placeholder`, `#wip`, `#canon`) work the moment you type them. You can search all tags via the tag pane in the right sidebar, or use the search bar with `tag:#unresolved` to find everything that needs attention.

### **How to view a table of contents of individual files in the sidebar?**

Enable the core plugin **Outline** if needed. Go to Settings → Core plugins → toggle on **Outline**. It appears in the right sidebar (View → Right Sidebar) and shows a clickable table of contents generated from your markdown headings (`##`, `###`, etc.) for whatever file you currently have open.