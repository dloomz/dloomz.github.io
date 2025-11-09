---
layout: /src/layouts/MarkdownPostLayout.astro
title: Maya Snippets - 2026 edition
author: Dolapo Okuboyejo
description: "A collection of maya snippets I've written."
image:
  url: "/images/posts/maya_snippets.webp"
  alt: "Branded image featuring maya logo next to text that says: Maya Snippets."
pubDate: 2025-11-09
tags:
  [
    "Maya", "Python", "Snippets"
   
  ]
languages: ["maya", "python", ]
---

I've decided to create a post that will have a collection of my snippets. This page will be updated throughout the year. I'm currently serving as Pipeline for my 3rd Year Film, so I'm finding myself writing quick tools for my team!

## Maya match size tool (wip)
---

A tool in maya similar to the Match size(y-min) tool in houdini. This ensures geometry will be level to the ground.

```python
import maya.cmds as cmds

sel = cmds.ls( selection=True )

for s in sel:
    bbox = cmds.exactWorldBoundingBox(s)
    
    cmds.move(0, bbox[1], 0,
            [f'{s}.scalePivot', f'{s}.rotatePivot'], 
            relative=False)
    
    ref = cmds.polyPlane(n='matchPlane')
    cmds.matchTransform(f'{s}',{ref[0]}, pos=True, rot=False, scl=False)
    
cmds.delete(ref) 
```

