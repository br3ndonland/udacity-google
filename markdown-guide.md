# Markdown guide

Brendon Smith

br3ndonland


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Intro](#intro)
- [Markdown syntax](#markdown-syntax)
  - [Syntactic suggestions](#syntactic-suggestions)
  - [Resources](#resources)
- [Markdown methods](#markdown-methods)
- [Markdown apps](#markdown-apps)
  - [Text editors](#text-editors)
  - [IDEs](#ides)
  - [Note apps](#note-apps)
  - [In-browser editors](#in-browser-editors)
  - [Social apps](#social-apps)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Intro

**Markdown is a syntax for easy generation of HTML pages from plain text files.** It has most of the functionality of HTML while being much easier to read, and is very widely used (for example, READMEs on GitHub).

Here's a comparison of the same code written in Markdown and HTML:

<img src="img/markdown-html-comparison.png" alt="Markdown and HTML comparison" width="75%">

When coding projects, I keep **computational narratives** describing what I do at each step, like journals or lab notebooks. I learned how to keep computational narratives from scientific computing in Jupyter Notebook/JupyterLab and RMarkdown. Computational narratives capture my train of thought, so I can retrace my steps, retain what I have learned, and teach others.

I have also been looking for an alternative to Evernote, with Markdown instead of rich text.

I hope this is helpful!

[(Back to TOC)](#table-of-contents)


## Markdown syntax

### Syntactic suggestions

Here are a few pointers:


#### File extensions

* Several different extensions can be used, including .md, .mdown, and .markdown.
* **I prefer to use .md for brevity and consistency.**


#### Headers

* Create headers with `#`. Each `#` increases header level (`##` is outline level two), up to six levels.
* **For organization, I reserve H1 (`#`) for the title of the file at the top. Major headers begin with H2 (`##`).**
* **For clarity, I leave one blank line after each header, and two blank lines before the next header.**
* I use the headers to create a **Table of Contents (TOC)** at the beginning of the files with [DocToc](https://github.com/thlorenz/doctoc). JupyterLab and RStudio have inline TOC displays ([see below](#jupyterlab)). **I add `## Table of Contents` before the TOC for navigation.**
* **I include [(Back to TOC)](#table-of-contents) links after each section for easy navigation back to the table of contents.** Simply write `[(Back to TOC)](#table-of-contents)`.


#### Text

* **Bold text:** use **double star at beginning and end of text to bold**
* **Italics:** *Single star with no space before and after.* _Underscores also work._
* **I prefer to indent Markdown text with tabs at two-space width.** Four spaces can be read by some systems as code blocks.


#### Lists

* **Lists should be preceded by a blank line.**
* Single `*`, `-`, or `+` at beginning of line, followed by tab or space.
	- Indent with tab for next outline level
		+ Like this

1. Ordered lists
2. Like this
	- And you can add in unordered lists.
	- Like this
3. Inside of ordered lists.


#### Code

You can include `inline code inside single backticks`

```text
Fenced code blocks inside triple backticks
```

* Code blocks can be indented to match your lists
	```text
	like this
	```
* In GitHub-Flavored Markdown, you can specify the language next to the first set of triple backticks for syntax highlighting:
	- Bash
		```bash
		$ git reset --hard
		$ git checkout origin/task-page-skeleton
		```
	- JavaScript
		```javascript
		// have new service worker take over right when refresh is pressed
		self.skipWaiting()
		
		// from a page
		reg.installing.postMessage({foo: 'bar'});
		
		// in the service worker
		self.addEventListener('message', function(event) {
			event.data; // {foo: 'bar'}
		});
		
		// when the new service worker has taken over, signal page reload
		navigator.serviceWorker.addEventListener('controllerchange', function() {
			// navigator.serviceWorker.controller has changed
			});
		```
	- Python
		```python
		name = input("Please type your name: ")
		print('Great job', name + '!', 'Keep practicing your Python!')
		```


#### File paths

* Local disk: use UNIX format file paths
* Dropbox URLs: **To use Dropbox links in Markdown, change the end of the link from dl=0 to dl=1.** In this way, images can be embedded and datasets can be referenced by URL without having to download a local copy.


#### Images

```text
![Alt text that appears below the image in the output](/path/to/img.jpg "Optional title that will show up when you hover over the image in the output")`
```

I still prefer to use HTML image tags, because they allow for more customization:

```text
<img src="/path/to/img.jpg" alt="Alt text" class="" width="75%">
```

[(Back to TOC)](#table-of-contents)


### Resources

* [MarkdownGuide](https://www.markdownguide.org/)
* [GitHub-Flavored Markdown](https://guides.github.com/features/mastering-markdown/)
* [Dillinger](https://dillinger.io/) is a helpful online Markdown editor with live preview.
* [Turndown](https://domchristie.github.io/turndown/) is an HTML to Markdown converter.
* [Udacity README course](https://www.udacity.com/course/writing-readmes--ud777)

[(Back to TOC)](#table-of-contents)


## Markdown methods

* When I begin a Udacity lesson, I create a new file in my text editor.
* I use `H1` for the title at the top, like `# Lesson 3. An Overview of Service Worker`.
* I usually reserve `H2` in case I want to break the lesson into different parts.
* I paste in the sections of the lesson from the Udacity interface, and set each one to `H3`.
	
	<img src="img/markdown-methods-lesson01.png" alt="Copying lesson sections from Udacity" width="300px">

* As I go through the lesson, I take notes on what I do in each step. My [notes from Lesson 3](https://github.com/br3ndonland/udacity-google/blob/master/udacity-google-03.md) are a helpful example.
	- If I write code, I include it with code blocks.
	- If I get stuck, I explain the steps I take to solve the problem. For example, I had a [Git issue during Lesson 3](https://github.com/br3ndonland/udacity-google/blob/master/udacity-google-03.md#311-quiz-hijacking-requests-1-quiz).
* At the end of the lesson, I use [DocToc](https://github.com/thlorenz/doctoc) to generate a Table of Contents from the headers.
* I write feedback and paste it into the feedback popup box in the Udacity lesson.

[(Back to TOC)](#table-of-contents)


## Markdown apps

### Text editors

Most code editors have extensions for Markdown.


#### Atom

[Atom](https://atom.io/) has good Markdown support. See the [Flight Manual](https://flight-manual.atom.io/using-atom/sections/writing-in-atom/) for instructions.


#### Sublime Text

I currently use [Sublime Text](http://www.sublimetext.com/) for most of my coding. It's fast, responsive, and packages give it powerful features.

Here's how to set up Sublime Text for Markdown:

* Install [Sublime Text](http://www.sublimetext.com/)
	- I like the Mariana color scheme and the Adaptive theme.
* Install [Package Control](https://packagecontrol.io/)
* Use Package Control from within Sublime Text to install:
	- MarkdownEditing
	- Markdown Preview
* Type sublimely in autocomplete bliss!

You can see my full setup, including keybindings, on [GitHub](https://github.com/br3ndonland/general/blob/master/computer-setup.md).


#### Visual Studio Code (vscode)

I haven't used vscode, but they provide helpful [instructions](https://code.visualstudio.com/Docs/languages/markdown) on how to configure it for Markdown.

[(Back to TOC)](#table-of-contents)


### IDEs

IDE = Integrated Development Environment


#### JupyterLab

* [JupyterLab](http://jupyterlab.readthedocs.io/en/latest/) is produced by [Project Jupyter](http://jupyter.org/). It is most widely used for scientific computing with Python, but supports many programming languages. It allows you to create "reproducible computational narratives," containing Markdown text interspersed with code chunks that you can run. JupyterLab was previously Jupyter notebook. They released [some awesome updates](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) that I'm looking forward to using.
* It is easiest to install JupyterLab through [Anaconda](http://jupyter.org/install).
* For examples of how to use Jupyter Notebook/JupyterLab, you can check out my [Python files](https://github.com/br3ndonland/udacity-fsnd/tree/master/01-fundamentals/python) from the Udacity Full Stack Web Developer Nanodegree program.


#### RStudio

* [RStudio](https://www.rstudio.com/) is an IDE for the R programming language, used mostly for statistics and data science.
* Like JupyterLab, RMarkdown documents contain Markdown text with functional R code chunks.
* I have written up a [guide to R](https://rpubs.com/br3ndonland/Rguide), and an [example of scientific data analysis](https://rpubs.com/br3ndonland/Rproteomics-2016-Nrf1), using RMarkdown. They're currently hosted on the free [RPubs](https://rpubs.com/br3ndonland) site, but I'm working on moving them over to GitHub so you can see the source code.

[(Back to TOC)](#table-of-contents)


### Note apps

#### [Bear](http://www.bear-writer.com/)

I found Bear via [M.G. Siegler in 500 words on Medium](https://500ish.com/@mgsiegler).

*Pros*

* Uses a modified syntax called Polar Bear.
* Supports internal relative links
* Tags and subtags
* Themes
* Evernote migration and import
* Writing tools, like word counts and read time


*Cons*

* Apple only
* Paid premium plan
* Not encrypted
* Collaboration features could be better. No shared notebooks.


#### [Day One](http://dayoneapp.com/)

Day One [supports Markdown](http://help.dayoneapp.com/tips-and-tutorials/markdown-guide).


#### [Dropbox Paper](https://www.dropbox.com/paper)

*Pros*

* Markdown
* Collaboration
* Sync
* Embedding works well


*Cons*

* Paper files don't show up in your regular Dropbox file structure
* No tags
* No themes
* PDFs embedded in Dropbox Paper documents don’t lead to the actual PDF when clicked, in the mobile apps.
* PDF thumbnails are too large when inserted as single PDFs. When two or more files are inserted, the thumbnails are next to each other and the size is more reasonable. Needs a "view as attachment" option like Evernote.


#### [Inkdrop](https://www.inkdrop.info/)

[Features](https://www.inkdrop.info/features): Markdown, themes, encryption, cross-platform. Seems to be like Bear, but cross-platform. Check out the developer's [Medium blog](https://blog.inkdrop.info).


#### [Jottings](http://jottingsapp.com/)

iOS note app with Markdown, tagging, and Dropbox sync.


#### [Laverna](https://laverna.cc/) 

*Pros*

* Encrypted
* Markdown
* Multimedia
* Internal linking
* Make tags with #tag
* Open source
* Built with Electron


*Cons*

* Evernote import?
* No Android app yet
* No dark themes yet
* No Markdown TOC


#### [Simplenote](https://simplenote.com/)

From WordPress

*Pros*

* Markdown support


*Cons*

* Evernote import?
* Multimedia?


#### [Standard Notes](https://standardnotes.org/getting-started)

*Pros*

* Simple, dependable text note app
* Note tagging
* Themes like solarized and dark
* Extensions to add features like Markdown
* Encrypted
* Backup to Dropbox and Google Drive
* "Built to last"


*Cons*

* Extensions only work on desktop and web.
* Can't attach files from mobile devices.
* Not great with multimedia. Tried to drag and drop a movie, and it just displayed the movie instead of my notes.
* [Evernote import](https://standardnotes.org/evernote): Formatting, images, and attachments will not be copied over. Have to break up .enex into 250 MB segments.
	- My response to email survey:
		> *Have you ever tried Standard Notes Extended?*
		> 
		> No. If I became a regular user, I would happily pay for Extended. I'm not regularly using Standard Notes because I'm heavily invested in Evernote. I've been using it for six years, and have a 4 GB database with ~4400 tagged notes. I would love to migrate from Evernote to another service, converting from rich text to Markdown and encrypting my data, while keeping my multimedia attachments. Bear is one example of this type of migration, but I don't use Bear because it's Apple-only.


#### [Turtl](https://turtlapp.com/)

[Turtl blog on Tumblr](http://turtlapp.tumblr.com/)

*Pros*

* Promising encrypted Evernote alternative
* Evernote import coming in 0.6.5
* Markdown
* Sharing
* Some multimedia support
* Android app


*Cons*

* Still needs more development
* No dark themes yet


#### [Typora](https://typora.io/)

*Pros*

* File list panel, allowing you to use any cloud service to sync.
* CSS configurable
* Support for images
* Document export
* Footnote feature is cool


*Cons*

* Feature-poor
* Not for android
* If it’s not for mobile and not multimedia, what’s the point beyond Sublime Text? Or Dillinger?


#### [Ulysses](https://ulyssesapp.com/)

*Pros*

* Nice interface
* Markdown
* Dark themes
* Can also manage journal articles and research


*Cons*

* Apple only
* Encryption?
* Moved to expensive subscription model
* Maintains article tags as "keywords," a fatal flaw shared by other apps like Papers


### In-browser editors

* [Dillinger](https://dillinger.io/): In-browser Markdown editor with live preview.
* [GitBook](https://www.gitbook.com/): Online platform for writing documentation. It combines and converts Markdown files into multimedia-enabled notebooks, like book chapters.
* [Gnotes](https://notes.giggy.com/): Write Markdown, save to Dropbox, see in Evernote. One-way only.
* [Markdown Here](https://markdown-here.com/index.html): Allows Markdown formatting for in-browser web apps like Gmail. See [GitHub](https://github.com/adam-p/markdown-here).
* [Marxico](http://marxi.co/):
	- In-browser Markdown editor based on Dillinger.
	- Works with images.
	- Has live TOC.
	- Renders well on mobile browsers, but only selection capability available is "select all".
	- May not have seamless integration with Evernote. [Comment from jefito](https://discussion.evernote.com/topic/99861-native-markdown-support/?do=findComment&comment=448394):
		> As far as I can tell, Marxico doesn't really support round-tripping MarkDown <--> Evernote. Once it's in Evernote, and you make changes there, then getting Markdown back can be problematic, since Evernote can use pretty full HTML. If it works for you, then that's great (or or if I'm not understanding their web site then please correct me), but let's be careful about turning this into something that it's not.
* [StackEdit](https://stackedit.io/): In-browser Markdown editor with live preview. Uses PageDown, the engine powering the Markdown capabilities of the Stack Exchange forums.

[(Back to TOC)](#table-of-contents)


### Social apps

#### Gitter

[Gitter](https://gitter.im/) uses Markdown formatting for chats. See their [Markdown basics](https://gitter.zendesk.com/hc/en-us/articles/200176682-Markdown-basics) support article.


#### Udacity discussion forums

You can use Markdown formatting in your forum posts. See GitHub for the source code.


#### ~~Slack~~

Slack uses a simplified pseudo-Markdown and has [stated](https://get.slack.help/hc/en-us/articles/202288908#a-note-about-markdown) that it will not be building in full Markdown capabilities.


[(Back to TOC)](#table-of-contents)