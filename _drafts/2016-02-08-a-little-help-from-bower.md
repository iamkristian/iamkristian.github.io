---
layout: post
title:  "A little help from bower"
date:   2016-02-08 13:30
categories: bower npm ubuntu
---


curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
sudo apt-get install -y nodejs


npm install -g bower


bower init

{
  "name": "filmguf",
    "version": "0.0.1",
    "authors": [
      "me@krx.io"
      ],
    "description": "A movie discussion service",
    "license": "MIT",
    "private": true,
    "ignore": [
      "**/.*",
    "node_modules",
    "bower_components",
    "test",
    "tests"
      ],

    "dependencies": {
      "bootstrap": "~3.1.1"
    }
}



.bowerrc
{
  "directory": "vendor/assets/components"
  }
