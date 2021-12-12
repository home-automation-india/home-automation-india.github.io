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
  
## Using the Github PR process
Everyone contributing to the repo requires a PR for every change. 
  
### Step 1 - Make a change
  * Start editing use the Github editor, but *do not* commit to the main branch. Always create a new branch for your change. Recommendation is to do smaller changes for easier review by others, don't make 100 files in a single PR. Branch name should be: `<username>-<readable name>`. Eg while using this guide I used `kunalgrover05-contributing-guide`
  * Editor requires you to make only one commit per file. It is okay because finally while merging we will squash them all into a single commit for your branch. 
  * Make changes to other files in the same branch and keep adding good Commit messages. They will help you later. 
  
### Step 2 - Get a peer review
  * Every change requires atleast one approval from another member of this repository. If you receive some feedback, you can address it using details in Step 1. 
  
### Step 3 - Merge your changes
  * Merge your changes using Squash and merge. Here you can create a good commit message using all the commits you created in Step 1. 
