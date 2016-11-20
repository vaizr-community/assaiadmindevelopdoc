# MkDocs

## Usage of MKDocs

For now MKDocs is used to create and maintain the development documentation. When start working with MKDocs for documenting Assai there are a couple of things which should be considered and checked. If you never worked with MarkDown consider reading [https://daringfireball.net/projects/markdown/](https://daringfireball.net/projects/markdown/). If you never worked with MKDocs consider reading [http://www.mkdocs.org](http://www.mkdocs.org). The contents of this site are also saved in the root directory of the devdoc Mercurial repository as a pdf file mkdocs.pdf

The document assai9_poc_global_design.md is added as example on how to use MKDocs

The title of the document you should repeat in the document itself

     # Assai-9 POC global design

This exact name you should use in the mkdocs.yml file as title as reference you should the name in the file structure.

          -
                ? "Assai-9 POC global design"
                : reference/design/assai9_poc_global_design.md

A document which is not added to the mkdocs.yml can not be referenced to

For the rest the assai9_poc_global_design.md should explain itself. During work check the look and feel, within your IDE you can check your work with a markdown plugin and you can check the final result with the following command

    ﻿C:\workspaces\assai\devdoc>mkdocs serve

and then you can go to http://localhost:8000

## Installation

You can install MKDocs with **pip. pip** is a package management system used to install and manage software packages written in Python. pip is already installed together with you python installation.

    C:\workspaces>pip install mkdocs


## Verify MKDocs

    C:\workspaces>mkdocs --version
    mkdocs, version 0.15.3

