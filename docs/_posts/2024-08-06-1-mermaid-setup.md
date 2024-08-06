---
layout: post
title: "Setting up mermaid diagram for Jekyll"
date: 2024-08-06 15:56:00 +0800
categories: []
---

I did not find any updated posts as to how to setup mermaid js for diagraming without usage of any plugins. I have tried to use several other samples I found but I could not get it to work as it required jquery and my site did not come configured with it

After some digging, it looks like mermaid js version 10 has new ability to configure a custom query selector, which omits the need of any hacks/workarounds, which can be found in their docs [here](https://mermaid.js.org/config/usage.html#using-mermaid-run)

In any case, the way I have done mine is by adding the following lines into my footer template

```html
<script src="https://cdn.jsdelivr.net/npm/mermaid@10.9.1/dist/mermaid.min.js"></script>
<script>
    mermaid.initialize({ startOnLoad: false });
    mermaid.run({
        querySelector: '.language-mermaid',
    });
</script>
```

This will then now render the following below:

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```  