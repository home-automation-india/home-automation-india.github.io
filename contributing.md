---
layout: default
title: Contributing
nav_order: 99
---

## Principles
- Open documentaton: By design everything is read accessible to everyone on the planet
- Trust but maintain quality: Everyone who wants gets added with write permissions. However committing to main branch requires atleast 1 review to get their PRs merged. I am trusting the group as a whole to maintain high bar on quality when approving PRs.
- Well organized: We do a lot of things and everyone has different interests. We expect this repo to represent all of these over time but we still want it to be well organized for newbies. The [contributing guidelines](https://home-automation-india.github.io/contributing.html) will keep updating to reflect the standards for best organization, please follow them. 
- GPL v3 licensed: We spend time out of busy lives to build this documentation, we don't want people to use it and distribute as their product. All content is free and open source. 
- Don't violate copyrights: Since this is publicly visible, we have more responsibility to not violate copyrights of others. Don't include images/videos with licenses without providing sufficient attribution. Link instead of downloading and sharing as your own. 



## Pre-requisites:
### Learn Markdown
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
For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) or [Markdown cookbook](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

### Using Github editor
Be comfortable in creating and editing files using the [Github Editor](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files)

### Learn about Github branches and PR process
Everyone contributing to the repo requires a PR for every change. Every PR requires atleast one approval from another member in this repo.   
  
#### Step 1 - Make a change
  * Start editing use the Github editor, but **do not** commit to the main branch. Always create a new branch for your change. Recommendation is to do smaller changes for easier review by others, don't make 100 files in a single PR but similar related ones. Branch name should be: `<username>-<readable name>`. Eg while using this guide I used `kunalgrover05-contributing-guide`.
  * Github Editor requires you to make only one commit per file. It is okay because finally while merging we will squash them all into a single commit for your branch. 
  * After you make your first commit, switch to using the branch you just created using these [instructions](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/making-changes-in-a-branch/managing-branches#switching-between-branches).
  * Make changes to other files in the same branch and keep adding good commit messages for everything. They will help you later. 

#### Step 2 - Raise a Pull Request
   * Raise a pull request by going [here](https://github.com/home-automation-india/home-automation-india.github.io/pulls) and click on "New pull request". You can read more about PRs in this [guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).
 
#### Step 3 - Get a peer review
  * Every change requires atleast one approval from another member of this repository. If you receive some feedback, you can address and make additional Step 1. Your PR should automatically get updated with new commits in your branch.
  
#### Step 4 - Merge your changes
  * Merge your changes using Squash and merge. Here you can create a good commit message using all the commits you created in Step 1. 

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
