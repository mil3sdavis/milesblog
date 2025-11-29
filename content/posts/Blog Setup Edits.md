---
title: 003 - Blog Setup Edits
date: 2025-11-29
draft: false
tags:
  - blog
---

This blog was setup based on instructions provided by #NetworkChuck @ https://www.youtube.com/watch?v=dnE7c0ELEH8

I had to made a a few edits to his process/script to make it work for what I wanted to do. He wrote a python script which was intended to transfer images from an #Obsidian vault, but it only accounted for PNG files, I modified the regex to account for JPEG/JPG and GIFs also. 

Regex edit for image.py
```
        # Step 2: Find all image links in the format ![Image Description](/images/Pasted%20image%20...%20.png)
        #images = re.findall(r'\[\[([^]]*\.png)\]\]', content)
        images = re.findall(r'\[\[([^]]*\.(?:png|jpg|jpeg|gif))\]\]', content, re.IGNORECASE) 
```


NetworkChuck also didn't explain the process for setting up auto deploy on Hostinger which requires setting up a webhook from Hostinger that is triggered when a post is uploaded to GitHub.