---
title: "How I Built My Website with Hugo and GitHub Pages"
date: 2023-07-15T10:00:00+05:30
draft: false
description: "Step-by-step guide to building a personal website with Hugo and GitHub Pages."
tags: ["Hugo", "GitHub Pages", "Static Sites", "Web Development"]
categories: ["Web Development"]
cover:
  image: "hugo.png"
  alt: "Hugo and GitHub Pages"
  caption: "Building a website with Hugo and GitHub Pages"
  relative: false
---

## Introduction

Creating a personal website is an essential step for developers, bloggers, and professionals who want to showcase their work online. I built my website using Hugo, a fast and flexible static site generator, and hosted it on GitHub Pages. In this blog, I'll walk you through the process, covering everything from setting up Hugo to deploying the site.

## Why I Chose Hugo

Hugo is a powerful static site generator that offers several advantages:

- **Speed**: It compiles sites in milliseconds
- **Flexibility**: It supports themes, content organization, and customizations
- **Ease of Deployment**: Static sites work seamlessly with GitHub Pages

## Setting Up Hugo

### Prerequisites

Before starting, you need to have the following installed:

- Hugo (v0.80.0 or higher)
- Go (v1.16 or higher)
- Git

### Installing Hugo

To install Hugo, use the following command:

```bash
brew install hugo  # macOS
sudo apt install hugo  # Linux
choco install hugo  # Windows (using Chocolatey)
```

### Creating a New Hugo Site

Once Hugo is installed, create a new site:

```bash
hugo new site my-website
cd my-website
```

### Choosing a Theme

For my site, I chose the PaperMod theme, a clean and minimalistic option. To install it, run:

```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

Then, update the config.yaml file to use PaperMod:

```yaml
theme: "PaperMod"
```

## Customizing the Website

### Configuring config.yaml

I updated my config.yaml to include basic settings, such as:

```yaml
baseURL: "https://darshandev.me/"
title: "Darshan Prajapati"
menu:
  main:
    - identifier: blogs
      name: Blogs
      url: /blogs/
      weight: 10
    - identifier: projects
      name: Projects
      url: /projects/
      weight: 20
    - identifier: about
      name: About
      url: /about/
      weight: 40
```

### Adding Content

I structured my content into categories such as blogs, projects, and about by placing Markdown files under content/:

```bash
hugo new blogs/my-first-blog.md
```

This creates a new post in content/blogs/.

### Configuring SEO

To optimize SEO, I added the following metadata to my posts:

```yaml
title: "How I Built My Website with Hugo"
description: "Step-by-step guide to building a personal website with Hugo and GitHub Pages."
tags: ["Hugo", "GitHub Pages", "Static Sites"]
categories: ["Web Development"]
```

## Hosting with GitHub Pages

### Setting Up GitHub Repository

I created a GitHub repository and pushed my Hugo project:

```bash
git init
git remote add origin https://github.com/thedarshannn/thedarshannn.github.io.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

### Deploying to GitHub Pages

I automated deployment using GitHub Actions by adding `.github/workflows/hugo.yml`:

```yaml
name: Deploy Hugo site to Pages
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"
      - name: Build
        run: hugo --minify
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

This workflow builds the site and deploys it to GitHub Pages.

### Setting Up a Custom Domain

I linked my domain darshandev.me by adding a CNAME file in the static/ folder with my domain name.

## Conclusion

Building my website with Hugo and GitHub Pages was a smooth process. Hugo's flexibility, PaperMod's minimalism, and GitHub's seamless deployment made it easy to launch my site. If you're looking for a fast and reliable way to build your personal website, I highly recommend this setup.

Let me know if you have any questions or need help setting up your own site!
