# The _Match Documentation_ Website 

This repository contains the code for creating the CPJKU Documentation website.
You can find the latest version of the website on [https://cpjku.github.io/docs/](https://cpjku.github.io/docs/). 


### General Instructions 

When you change a file and push your changes then the website will be automatically updated.
The website is created using the Hugo Book Template Theme and Wowchemy.
A github action builds this page to the gh-pages branch.


Hugo extended 0.83.1 is required to build this website. You can download it [here](https://github.com/gohugoio/hugo/releases/tag/v0.83.1)

To view your changes locally use:
```shell
cd To/repository/Parent/directory/docs/

hugo server
```
You can copy `//localhost:1313/` in your browser to visualize locally the website and your ongoing changes.

## Repository Organization

#### Content

In the folder content of the repository one can find the complete contents of the created website.
This is the principal folder that should be mainly used and changed.  
Every folder in this directory page should correspond to a Page accessible by the main page. 
Following this logic, there is a folder home for the main (_welcome_) page, a folder about match documentation,
a folder about partitura documentation or redirection, and also could have matchmaker documentation or other projects in distinct folders.


#### Assets 
The asset folder contains media such as icons, logos, etc.

#### Date and Resources

These folder contain Theme related information that is used automatically to create a hugo style website. They

#### Config

The config folder concerns language and other configuration related settings.

## Theme, Wowchemy & Hugo related Information

- 👉 [**Get Started**](https://wowchemy.com/templates/)
- 📚 [View the **documentation**](https://wowchemy.com/docs/)
- ⬆️ **Updating Wowchemy?** View the [Update Guide](https://wowchemy.com/docs/update/) and [Release Notes](https://wowchemy.com/updates/)
