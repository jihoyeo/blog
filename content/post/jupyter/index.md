---
authors:
- admin
categories:
  - Python
date: "2019-02-05T00:00:00Z"
draft: false
featured: false
image:
  caption: ""
  focal_point: ""
projects: []
subtitle: Learn how to blog in Academic using Jupyter notebooks
summary: Learn how to blog in Academic using Jupyter notebooks
tags: []
title: Display Jupyter Notebooks with Academic
---

Jupyter notebook을 blogdown을 통해 post로 등록하는 방법에 대해 기록해두고자 한다.

[이곳](https://www.timlrx.com/2018/03/25/uploading-jupyter-notebook-files-to-blogdown/)의 링크를 기반으로 작성하였다.


## Convert notebook to Markdown

Go directory where the ipynb file is located. For example

```bash
cd C:/Users/User/jupyter/
```

Convert ipynb to markdown

```bash
jupyter nbconvert --to markdown scipy.ipynb
```
This generates a .md file as well as a folder containing all the images from that file.  
In my case the folder was named scipy.

Then, copy the image files to the static folder where the website is located. I placed my files in the static/img/post_name folder.


## Edit your post metadata

1. Add new post with R Markdown. Set post name, category, tag. 

2. Copy the markdown file over, and replace all the image directory paths to point to the newly created one in the static folder.


