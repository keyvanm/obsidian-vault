---
url: https://gist.github.com/badarotti/ee7ba3f5aab6741ad630a1996521ad67
---

> [!Notes]
>The information and setup explained here was collected from the forum and GitHub issues, thanks everyone.
>
>I only tested this hack on Linux / Firefox. Please post below your experience with other OS / browsers. Thank you.

## The extension

[MarkDownload](https://github.com/deathau/markdownload) is a non Obsidian specific extension to save web clippings on your file system in Markdown format. Obsidian integration has been added to the extension to save web clippings to a preset folder in an Obsidian vault.

This is a great extension that works as advertised, and I appreciate the work that went into it. However, the Obsidian integration, even though it works, leaves a couple of things to be desired for a seamless workflow.

- The extension integration does not save any images along with the web clippings, even tough the extension does so standalone. I often need to save the images with the page so I'd like to have the option
- Even when using the extension without the Obsidian integration, it will only save the images if saving in the user's system download folder. If you try to save elsewhere, the images are not saved no matter what you do.
- The Obsidian integration is hidden in the right-click context menu, something that's not documented and ended up puzzling every new user I tried to onboard

## The Aim of this configuration

- To be able to send a page **with images** to Obsidian with the a simple click on the extension toolbar icon using the symbolic link hack explained below
- To be able to send a **text only** page to Obsidian with the right-click menu in the page or on the toolbar icon using the extension Obsidian integration which requires the install of the Obsidian extension [Obsidian Advanced URI](https://vinzent03.github.io/obsidian-advanced-uri/)
- To quickly save web clippings, with or without images, in an Obsidian vault folder called `inbox` to later manage and organize the clippings from within Obsidian.
- The saved clippings should be saved in a markdown file. The clipped images will be saved in a directory alongside the markdown file with the same name minus the `.md` extension. This will make it easy to edit/move/delete the markdown file along with its resources.

```
obsidian_is_great_article.md  < markdown file
obsidian_is_great_article     < folder containing the article images
```

## How-to

Luckily, the setup is easy, it just requires a few steps.

### In Obsidian

- Install the [Obsidian Advanced URI](https://vinzent03.github.io/obsidian-advanced-uri/) plugin
- Create the `inbox` folder where clippings will be saved.

### In your browser

- Install the MarkDownload extension: [Firefox](https://addons.mozilla.org/en-GB/firefox/addon/markdownload/), [Google Chrome](https://chrome.google.com/webstore/detail/markdownload-markdown-web/pcmpcfapbekmbjjkdalcgopdkipoggdi), [Microsoft Edge](https://microsoftedge.microsoft.com/addons/detail/hajanaajapkhaabfcofdjgjnlgkdkknm) and [Safari](https://apple.co/3tcU0pD). More info can be found on the [extension GitHub page](https://github.com/deathau/markdownload).
- In the browser extension's preferences, set:
	- Always show Save As dialog: OFF
	- Download Images alongside markdown files: ON
	- Enable Obsidian Integration: Specify your vault name and `inbox` as the obsidian folder - This will give you the the right-click option to save without images
	- Set Folder inside Downloads/ to: `MarkDownload` - This is the only place where the extension seems to be able to save images
	- Set Download images alongside markdown files: `{pageTitle}/` - This will save the images in a folder named with the page title just like the markdown file.

### In your file system

If you're not familiar with the concept of Symbolic Links, this will take more time to explain than to do. It's just one command though.

If we use this setup as is, we will save the clippings in the `MarkDownload` folder in your system's download directory, not where we want them. Since we have to save in the Download directory for images to be saved, we will create a [Symbolic Link](https://en.wikipedia.org/wiki/Symbolic_link) from the `inbox` folder in your vault that targets the `MarkDownload` folder in your download folder.

Simply explained, this means that we instruct the operating system to regard both directories as one, but actually store the data in `inbox`. The `MarkDownloader` folder is just a symbolic link that points to  `inbox` which is the real folder that will actually hold the files. The extension will think it's using the download folder and will happily save the images in it, and Obsidian will be happy since it will have all the clippings and images in its vault.

#### On most operating systems
Most GUI file managers will let you create a symbolic link, so check your OS documentation or the articles I linked below. Just make sure that the symbolic link directory is the one in the download folder, and the real directory where the content will live is the one in your Obsidian vault.

#### Linux and Mac command line option
Be sure to use the correct paths
```bash
ln -s ~/home/user~/Obsidian/vault/inbox ~/Downloads/obs-personal
```

**"How-To Geek" help guides:**

Windows: [The Complete Guide to Creating Symbolic Links on Windows](https://www.howtogeek.com/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/)
Mac: [How to Create and Use Symbolic Links on a Mac ](https://www.howtogeek.com/297721/how-to-create-and-use-symbolic-links-aka-symlinks-on-a-mac/)
Gnome on Linux: [How to Create and Use Symbolic Links on Linux](https://www.howtogeek.com/287014/how-to-create-and-use-symbolic-links-aka-symlinks-on-linux/)

> [!question]
> Can anybody find an article for KDE?

## Usage

### To save with images

You can clip the whole page or a selection. Click the extension toolbar icon, review the Markdown that will be saved in the preview window, then click `Download`.

### To save without images

Right-click on the extension toolbar icon or on the page, select:
`MarkDownload - Markdown Web Clipper` > `Send Tab to Obsidian`

## Optional customization

You can customize the text properties the extension puts in the YAML Front-matter as well as the body of the markdown files. This can be done in the Template section in the extension browser configuration.

- I removed the `tags` properties since clipped web pages can have a inordinate number of tags that Obsidian will include in your vault tags. If you curate  your tags this will drive you crazy :)
- The extension puts the `url` property in the Front-matter, I added it again in the body of the markdown file so it will be visible and I can click on it easily.
- In use the filename as # (H1) in my vault so I removed the `{pagetitle}` from the body of the file to avoid duplication

Here's the template I currently use:

```yaml
---
created: {date:YYYY-MM-DD - HH:mm}
url: {baseURI}
author: {byline}
---
URL: {baseURI}
> ## Excerpt
> {excerpt}
---
```

Hope this helps,
A.B.

## Reference
- [markdownload GitHub project](https://github.com/deathau/markdownload)
- [markdownload User guide - GitHub](https://github.com/deathau/markdownload/blob/master/user-guide.md#markdownload-user-guide)
- [Obsidian Advanced URI](https://vinzent03.github.io/obsidian-advanced-uri/) - [GitHub](https://github.com/Vinzent03/obsidian-advanced-uri)
- [The Complete Guide to Creating Symbolic Links on Windows](https://www.howtogeek.com/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/)
- [How to Create and Use Symbolic Links on a Mac ](https://www.howtogeek.com/297721/how-to-create-and-use-symbolic-links-aka-symlinks-on-a-mac/)
- [How to Create and Use Symbolic Links on Linux](https://www.howtogeek.com/287014/how-to-create-and-use-symbolic-links-aka-symlinks-on-linux/)
