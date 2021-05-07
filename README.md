# wiki

Comprehensive NDC documentation https://ndclab.github.io/wiki/

## Git Workflow 

![ndcworkflow](https://user-images.githubusercontent.com/26397102/115577429-0b145300-a28a-11eb-9487-423750fd981a.png)

Folder/branch organization should follow this convention:

`->gh-pages`
- Up to date and live production branch with properly reviewed changes
- *no direct commits*

`->gh-pages-feature-[featureName]`
- Ongoing development and testing of feature to be pull requested into `gh-pages` 
- *no direct commits*

`-->gh-pages--[featureName]-[yourName]`
- *only* branch available for personal development, must be branched off of `gh-pages-feature-[featureName]` branch
- Merged into `-->dev-feature-[featureName]` after a pull-request (code review)

## Directory/Navbar Structure 

```yml
wiki
├── _sass
├── docs
|    ├──Onboarding
|    ├──_assets
|    ├──general-information
|    ├──project-specific-docs
|    ├──technical-docs
|    ...
├── LICENSE
├── _config.yml
├── index.md
├── ndcwikiicon.png
...
```

* `_sass`
    * Contains sass styling files that control the color-scheme, font, and other NDC wiki styles ([light guide to sass](https://sass-lang.com/guide))

* `docs`
    * directory that details the navbar structure. Pages and sub-pages reside here.

    * `Onboarding`
        
        * `onboarding.md`
        * `accessing-hpc.md`
        * `certifications.md`
    
    * `docs/_assets`
        * images of the ndc wiki

* `_config.yml`
    * yaml file that details wiki meta-data (title, theme, logo, etc) 

* `index.md`
    * Home-page content
    ![image](https://user-images.githubusercontent.com/26397102/115584943-ce982580-a290-11eb-9f54-8d9b94957e21.png)

## Guide to Website Development

Jekyll theme detailed in original [developer repo](https://github.com/pmarsceill/just-the-docs)


### Page Creation 

To create a page on the wiki and link it to the left-hand navigation bar, create the markdown file inside of the [docs/](https://github.com/NDCLab/wiki/tree/gh-pages/docs) directory and specify its' position on the navbar in the header.  

```yml
---
layout: default
title: <title>
nav_order: <navbar-ordinal>
---

# <title>
```

#### Working Example

The *contributing* tab on the wiki is placed on the 6th position in the navbar by specifying the following header in the [docs/contributing.md](https://github.com/NDCLab/wiki/blob/gh-pages/docs/contributing.md) file: 

```yml
---
layout: default
title: contributing
nav_order: 6
---

# Contributing 
// Rest of file continues here 
```

![image](https://user-images.githubusercontent.com/26397102/115580335-98f13d80-a28c-11eb-8fc2-e382e534d625.png)

### Parent & Child Page Creation 

To create a page/tab that contains sub-pages, create a directory inside of [docs/](https://github.com/NDCLab/wiki/tree/gh-pages/docs) named after the page/tab you plan on creating.

For example, to add a tab called `A` on the wiki navbar, create directory `docs/A/`. 

Next, create a markdown file inside of this directory and specify its position on the navbar and set the `has_children` tag to be `true`. 

```yml
---
layout: default
title: <title>
nav_order: <navbar-ordinal>
has_children: true
---

# <title>
```

To create child pages located underneath this parent page, create a markdown file also located in this directory and specify the parent title in the header: 

```yml
---
layout: default
title: <title>
parent: <parent-title> 
nav_order: <navbar-ordinal>
---

# <title>
```

#### Working Example

The *onboarding* tab on the wiki contains the child *accessing the hpc* in the navbar by specifying the following header in the [Onboarding/onboarding.md](https://github.com/NDCLab/wiki/blob/gh-pages/docs/Onboarding/onboarding.md) file:

```yml
---
layout: default
title: Onboarding
nav_order: 2
has_children: true
permalink: /docs/onboarding
---

# Onboarding
```

and the following directory structure:
```yml
wiki
...
├── docs
|    ├──Onboarding
|    |      ├── onboarding.md
```

followed by the [Onboarding/accessing-hpc.md](https://github.com/NDCLab/wiki/blob/gh-pages/docs/Onboarding/accessing-hpc.md) header: 

```yml
---
layout: default
title: Accessing the HPC
parent: Onboarding
nav_order: 2
---

## Accessing the HPC
```

located in the `docs/Onboarding/` directory

```yml
wiki
...
├── docs
|    ├──Onboarding
|    |     ├── onboarding.md
|    |     ├── accessing-hpc.md
```

![image](https://user-images.githubusercontent.com/26397102/115582028-28e3b700-a28e-11eb-9d05-1ac32db43609.png)
