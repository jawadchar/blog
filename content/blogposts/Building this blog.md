---
title: Building this blog
date: 2026-02-22
draft: false
tags:
  - blog
  - hugo
---



## Problems encountered 

- Hugo-extended is required for the theme I am using (hugo-blog-awesome). Confirm hugo-extended is installed with:!![Image Description](/images/Pasted%20image%2020260222121507.png)

- Transpiling Sass to CSS was required for the particular theme I am using (hugo-blog-awesome), so installation of Dart Sass is required. LibSass was deprecated in 0.153.0, so we use Dart Sass instead which is compatible with any Hugo version.
	-  Install sass with chocalatey:
	 ```choco install sass```

- We get a site rendering error using this theme because `.Site.Author` was deprecated in Hugo v0.124.0 and has been removed in newer versions. We need to update our template and config files to use the modern `[params.author]` convention.
 !![Image Description](/images/Screenshot%202026-02-22%20140914.png)

 To fix this, update your hugo.toml file to:
```
[params.author]
  name = "Your Name"
  email = "your@email.com"
```

Then update your Template (`rss.xml`):  
Change every reference from `.Site.Author.email` to `.Site.Params.author.email`. In my case, I had three.

- **Find:** `{{ .Site.Author.email }}`
- **Replace with:** `{{ .Site.Params.author.email }}`

Finally, restart your blog with `hugo server -t hugo-blog-awesome`.