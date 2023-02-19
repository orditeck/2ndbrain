---
created: 2023-02-12
modified: 2023-02-13
---
I started using Obsidian a few weeks ago and loved it right away. I then contemplated the idea of publishing online. I had a blog in the past but it felt different. Obsidian felt like that was it.

I took a look at the official [Publish](https://obsidian.md/publish) service from Obsidian but as a fellow Home Lab-er, there is no way I'd pay to host a personal website. I'd rather spend countless hours hacking something.

I started searching online for an "Obsidian Publish open source alternative" and found quite a few:
- [MindStone](https://mindstone.tuancao.me/): free open-source alternative solution to Obsidian Publish
- [pubsidian](https://github.com/yoursamlan/pubsidian): An Obsidian-Publish alternative but it's FREE
- [TuanManhCao/digital-garden](https://github.com/TuanManhCao/digital-garden) : Free Obisidian Publish alternative, for publishing your digital garden.
- [Markbase](https://www.markbase.xyz/): Easily sync and publish your docs, notes, and digital gardens
- [Quartz](https://quartz.jzhao.xyz/): Host your second brain and digital garden for free (based on Hugo)
- [binnyva/gatsby-garden](https://github.com/binnyva/gatsby-garden/): A Digital Garden Theme for Gatsby. Gatsby Garden lets you create a static HTML version of your markdown notes
- [Obsidian to Github](https://michalkorzonek.com/obsidian-to-github): Create and edit a Jekyll website in Obsidian. Publish to Github without friction.
- [ppeetteerrs/obsidian-zola](https://github.com/ppeetteerrs/obsidian-zola): A no-brainer solution to turning your Obsidian PKM into a Zola site.

None of them are perfect. The official Publish service isn't perfect neither.

[obsidian-zola](https://github.com/ppeetteerrs/obsidian-zola) was my favorite. It seemed simple enough, yet packed with features. I decided to give it a go. I had a few issues/bugs and noticed there wasn't much recent activity on the repo, so I started looking at the [Network graph](https://github.com/ppeetteerrs/obsidian-zola/network) to see which forks seemed active. 

I lent on [Yarden-zamir/obsidian-zola-plus](https://github.com/Yarden-zamir/obsidian-zola-plus), which adds a preview pop-up from another fork, giscus comments (which I didn't know was a thing), etc. 

I started using it and quickly noticed a few bugs. Enough to bother me. However, this time, I decided to create [my own fork](https://github.com/orditeck/cheap-publish) and start there, because why not. I'm now calling it Cheap Publish, 'cause my mom raised me an honest man.

So what did I change?

## More flexible frontmatter
I added the following frontmatter keys:
- `title`: allows to override the page's title without changing the filename
- `created`: shows the date the page was initially created, eg: `Posted February 13, 2023` 
- `modified`: when present and `modified != created`, shows both dates, eg: `Posted February 1, 2023, last updated February 5, 2023`

While working in that section, I re-enabled the read time:
> ![[Pasted image 20230212223136.png|Test|400]]

### Extra
I'm also passing down to `zola/templates/content/page.html` any `extra` frontmatter keys. Useful to customize the template based on that.

## Ability to bypass the landing page
I didn't read much about it, but Zola treats the homepage as a "special page". I just wanted a regular page from my note.

This is now possible. I'm not 100% sure the landing page still works to be perfectly honest with you, so if you try my fork and keep the landing page, please let me know 😬. 

To bypass the landing page, set `REDIRECT_HOME` in your `netlify.toml` to the path you want to redirect to, e.g. `REDIRECT_HOME = "README"`. It simply sets the main section's `redirect_to` setting to whatever you put in there. Zola doc [here](https://www.getzola.org/documentation/content/section/).

## Resize images
That one was bothering me a lot since it's supported natively in Obsidian.

Example of this above image resized to 100 pixels wide:

```md
![Engelbart|100](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)
or
![100](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)
```

![Engelbart|100](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg) or ![100](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)

Note that this is done dynamically in JavaScript because I was lazy, and it only supports the syntax above. 

## A few fixes/changes
- The sidebar no longer reload the whole page when clicking a link / anchor
- The graph no longer jumps on the first hover. It's also prettier with a little wiggling animation on load 😻.
- Removed mandatory `/docs` from every URLs, now directly served at `/`
- Removed `frontmatter=never` from `local-run.sh` (why!?)
- Fixed the URL detection for previews using the host (might not be a solution for all)
- Updated `obsidian-export` to its latest version
- Allowed `.` in filename, e.g. `1. Start here`, `2. Once Upon A Time`, etc. Useful for the sidebar since it's sorted by name.
- Better `blockquote` style

> "I have not failed. I've just found 10,000 ways that won't work." 
> <sup>- Thomas Edison</sup>

## TODO
- Fix the graph when URL contains a `#` (current node doesn't seem set)
- Identify external link
- Open external link in new window

## Wish list
- Better support for resized images 
	- [Obsidian doc](https://help.obsidian.md/How+to/Format+your+notes#Resizing+images)
	- [Discussion on obsidian-export](https://github.com/zoni/obsidian-export/discussions/59)
- Sort sidebar by using a frontmatter key