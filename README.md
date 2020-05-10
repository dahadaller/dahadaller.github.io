# CCNY_Prep

This is a Blog meant to keep track of our interview preparation progress. 

This GitHub Pages blog relies on:
- [travis-ci.org](https://travis-ci.org) for automating the update and generation process
- ['pelican'](https://blog.getpelican.com/) for static rendering of your blog from the markdown or asciidoc articles
- ['Elegant'](https://github.com/Pelican-Elegant/elegant) for the 'Theme'
- [peru](https://github.com/buildinspace/peru) for automating repository upgrades for plugins, etc
- [blog-o-matic](https://github.com/iranzo/blog-o-matic/blob/master/README.md)


## Setup

First, clone the repo.

```bash
git clone https://github.com/dahadaller/dahadaller.github.io.git

```

Then, checkout the `source` branch. You will be working exclusively in this branch. 
```bash
git checkout source
```


## Posting to Blog

Each member of the group has a designated folder in the `content/` directory. Any [markdown](https://www.markdownguide.org/cheat-sheet/) files placed in this directory will be turned into blog posts.

```
dahadaller.github.io/content
                        ├── Alex
                        ├── Angelique
                        ├── David
                        └── Kieran
```



Once you've written your new article in your `content` subfolder, perform:

~~~sh
## Add file to repository
git add content/<your_name_here>

## Add file to commit
git commit -m "Added my new article"

## Upload changes to github
git push
~~~

After some seconds, - [travis-ci](https://travis-ci.org) build the site with Pelican and commit the resultant html files to the master branch of this repo. After that, GitHub Pages will make the updated blog available at [dahadaller.github.io](https://dahadaller.github.io/).


## Blog Post Format

Generally, blog posts can be about any topic you think would be helpful to the group, and can be written in any way you choose. However, blog posts that are in response to the weekly excercises need to have certain headers in the YAML preamble so that Pelican can categorize them correctly on the final site. For example, a post made in response to [Week 1 Excercises](https://dahadaller.github.io/blog/2020/05/09/week-1-excercises/) would have a YAML headers like this:

```markdown
Title: David's Week 1 Excercises
Date: 2020-05-09 11:15
Authors: David Hadaller
Tags: Week 1

### Subtitle 

Rest of my post continues...

```
