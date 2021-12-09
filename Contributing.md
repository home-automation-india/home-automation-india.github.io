---
layout: default
title: Contributing
nav_order: 99
---

## How to Contribute to this Repo

You can use the [editor on GitHub](https://github.com/home-automation-india/home-automation-india.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

## Creating a new tutorial
A quick how-to for writing a new tutorial.
- Step 1: Find the appropriate subdirectory to place it, create one if it doesn't exist already (see instructions below).
- Step 2: Create a folder for your tutorial. You will use this folder to place all resources (images / YAML files etc.). Create a markdown file in this folder (maybe with the same name as folder).
- Step 3: Create the documentation using markdown.
- Step 4: Linking the doc in the navigation bar. Add the following to the top of your file. You can find the <ParentName> by going to the directory and looking for `index.md` file.
```
---
parent: <ParentNameGoesHere>
---
```

## Creating a new Parent
Create a new parent if you don't find any meaningful grouping to add your tutorial to.
- Step 1: Create a root directory for the parent. eg: create a directory called `linux`
- Step 2: Create `index.md` within the parent with the following content

```
---
has_children: true
title: <MeaningfulNameHere>
---
```
