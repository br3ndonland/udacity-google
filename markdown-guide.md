# Markdown guide

Brendon Smith

br3ndonland

## Table of Contents <!-- omit in toc -->

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

## Intro

**Markdown is a syntax for easy generation of HTML pages from plain text files.** It has most of the functionality of HTML while being much easier to read, and is very widely used (for example, READMEs on GitHub).

Here's a comparison of the same code written in Markdown and HTML:

<img src="img/markdown-html-comparison.png" alt="Markdown and HTML comparison" width="75%">

When coding projects, I keep **computational narratives** describing what I do at each step, like journals or lab notebooks. I learned how to keep computational narratives from scientific computing in Jupyter Notebook/JupyterLab and RMarkdown. Computational narratives capture my train of thought, so I can retrace my steps, retain what I have learned, and teach others.

I have also been looking for an alternative to Evernote, with Markdown instead of rich text.

I hope this is helpful!

[(Back to top)](#top)

## Markdown syntax

### Syntactic suggestions

Suggestions for standardized Markdown formatting have been provided by [markdownlint](https://github.com/DavidAnson/markdownlint) and [Markdown Style Guide](http://www.cirosantilli.com/markdown-style-guide/). Here are a few personal pointers:

#### File extensions

- Several different extensions can be used, including .md, .mdown, and .markdown.
- **I prefer to use .md for brevity and consistency.**

#### Headers

- Create headers with `#`. Each `#` increases header level (`##` is outline level two), up to six levels.
- **For organization, I reserve H1 (`#`) for the title of the file at the top. Major headers begin with H2 (`##`).**
- I use headers to create a **Table of Contents (TOC)** at the beginning of the file.
  - **I add `## Table of Contents` before the TOC for navigation.** I also include `<!-- omit in toc -->`, which tells the VSCode Markdown All In One extension not to put the `## Table of Contents` header itself into the TOC.
  - **I include [(Back to top)](#top) links after each section for easy navigation back to the top of the page.** Simply write `[(Back to top)](#top)`.
  - I add and auto-update TOCs in vscode with the [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) extension.
  - [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one), JupyterLab and RStudio provide inline TOC displays ([see below](#jupyterlab)).
  - Prior to vscode, I was adding and updating TOCs with [DocToc](https://github.com/thlorenz/doctoc) from the command line.

#### Text

- **Bold text:** use **double star at beginning and end of text to bold**
- **Italics:** *Single star with no space before and after.* Note that _underscores also work._
- **I prefer to indent Markdown text with two spaces.** Four spaces can be read by some systems as code blocks.

#### Lists

- **Lists should be preceded by a blank line.**
- Single `*`, `-`, or `+` at beginning of line, followed by tab or space.
  - Indent with tab for next outline level
    - Like this

1. Ordered lists
2. Like this
    - And you can add in unordered lists within ordered lists like this.
    - Adding an unordered list within an ordered list requires two levels of indentation.

#### Code

You can include `inline code inside single backticks`

```text
Fenced code blocks inside triple backticks
```

- Code blocks can be indented to match your lists

  ```text
  like this
  ```

- In GitHub-Flavored Markdown, you can specify the language next to the first set of triple backticks for syntax highlighting. Each language has a full name (like `python`), and an abbreviation (like `py`). The full list of supported languages can be found in [GitHub's Linguist repo](https://github.com/github/linguist), which is used to detect languages on GitHub. The *[languages.yml](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)* contains a list of the available abbreviations (called "extensions" in the YAML) for each language.
  - Shell

    ```sh
    git status
    git commit
    ```

  - JavaScript

    ```js
    // FizzBuzz from Trevor Dixon
    // https://stackoverflow.com/a/17623252

    const fizzBuzz = () => {
      for (let i = 1; i <= 100; i++) {
        let out = ''
        if (i % 3 === 0) out += 'Fizz'
        if (i % 5 === 0) out += 'Buzz'
        console.log(out || i)
      }
    }
    fizzBuzz()
    ```

  - Python

    ```py
    """
    FizzBuzz
    https://medium.freecodecamp.org/a-software-engineering-survival-guide-fe3eafb47166
    """


    def fizzbuzz():
        """Write a program that prints the numbers from 1 to 100.
        For multiples of three print 'Fizz' instead of the number.
        For multiples of five print 'Buzz'.
        For numbers which are multiples of both three and five print 'FizzBuzz'.
        """
        for i in range(1, 101):
            if i % 3 == 0 and i % 5 == 0:
                print("FizzBuzz")
            elif i % 3 == 0:
                print("Fizz")
            elif i % 5 == 0:
                print("Buzz")
            else:
                print(i)


    if __name__ == "__main__":
        fizzbuzz()

    ```

#### Images

```text
![Alt text that appears below the image in the output](/path/to/img.jpg "Optional title that will show up when you hover over the image in the output")`
```

**I still prefer to use HTML image tags, because they allow for more customization:**

```text
<img src="/path/to/img.jpg" alt="Alt text" class="" width="75%">
```

[(Back to top)](#top)

### Resources

- [MarkdownGuide](https://www.markdownguide.org/)
- [markdownlint syntax suggestions](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
- [Markdown Style Guide](http://www.cirosantilli.com/markdown-style-guide/)
- [GitHub-Flavored Markdown](https://guides.github.com/features/mastering-markdown/)
- [Dillinger](https://dillinger.io/) is a helpful online Markdown editor with live preview.
- [Turndown](https://domchristie.github.io/turndown/) is an HTML to Markdown converter.
- [Udacity README course](https://www.udacity.com/course/writing-readmes--ud777)

[(Back to top)](#top)

## Markdown methods

- When I begin a Udacity lesson, I create a new file in my text editor.
- I use `H1` for the title at the top, like `# Lesson 3. An Overview of Service Worker`.
- I usually reserve `H2` in case I want to break the lesson into different parts.
- I paste in the sections of the lesson from the Udacity interface, and set each one to `H3`.

  <img src="img/markdown-methods-lesson01.png" alt="Copying lesson sections from Udacity" width="300px">

- As I go through the lesson, I keep a computational narrative explaining what I do at each step.
  - I include code blocks to show the code I'm writing.
  - If I get stuck, I explain the steps I take to solve the problem.
- At the end of the lesson, I generate a Table of Contents from the headers.

[(Back to top)](#top)

## Markdown apps

### Text editors

Most code editors have extensions for Markdown.

#### Atom

[Atom](https://atom.io/) has good Markdown support. See the [Flight Manual](https://flight-manual.atom.io/using-atom/sections/writing-in-atom/) for instructions.

#### Sublime Text

Here's how to set up Sublime Text for Markdown:

- Install [Sublime Text](http://www.sublimetext.com/)
  - I like the Mariana color scheme and the Adaptive theme.
- Install [Package Control](https://packagecontrol.io/)
- Use Package Control from within Sublime Text to install:
  - MarkdownEditing
  - Markdown Preview
  - MarkdownLivePreview: Has some issues with lack of wrapping in the previews. See [GitHub Issue tracker](https://github.com/math2001/MarkdownLivePreview/issues/34).

#### Visual Studio Code (vscode)

**In my opinion, vscode is currently the best editor for working with Markdown.** Here's why:

- Built in live preview
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
  - TOC auto-generation and update
  - Live TOC in explorer panel
  - Easier keyboard shortcuts than Sublime Text (with the exception of hyperlink insertion, which I added with a [keybinding](https://github.com/neilsustc/vscode-markdown/issues/20))
- [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
  - Lints Markdown files based on style recommendations for standardizing code.

Full vscode configuration is available via [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) with [this public GitHub gist](https://gist.github.com/br3ndonland/01b625629ef98ec7a919a7b927d0ddaf).

[(Back to top)](#top)

### IDEs

IDE = Integrated Development Environment

#### JupyterLab

- [JupyterLab](http://jupyterlab.readthedocs.io/en/latest/) is produced by [Project Jupyter](http://jupyter.org/). It is most widely used for scientific computing with Python, but supports many programming languages. It allows you to create "reproducible computational narratives," containing Markdown text interspersed with code chunks that you can run. JupyterLab has [some awesome features](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) and was previously Jupyter notebook.
- It is easiest to install JupyterLab through [Anaconda](http://jupyter.org/install). It can also be installed from [Homebrew](https://brew.sh).
- For examples of how to use Jupyter Notebook/JupyterLab, you can check out my [Udacity Full Stack Web Developer Nanodegree program repo](https://github.com/br3ndonland/udacity-fsnd).

#### RStudio

- [RStudio](https://www.rstudio.com/) is an IDE for the R programming language, used mostly for statistics and data science.
- Like JupyterLab, R Markdown documents contain Markdown text with functional R code chunks.
- I have provided an example of scientific data analysis with R Markdown on [GitHub](https://github.com/br3ndonland/R-proteomics-Nrf1).

[(Back to top)](#top)

### Note apps

#### [Bear](http://www.bear-writer.com/)

##### Bear Pros

- This is one of the best Markdown note apps.
- Supports Markdown. Uses a modified syntax called Polar Bear.
- Tags and subtags
- Themes
- Syntax highlighting
- Supports internal relative links
- Evernote migration and import
- Writing tools, like word counts and read time
- Reasonably-priced subscription plan

##### Bear Cons

- Apple only. Need Android app.
- Not encrypted
- Collaboration features could be better. No shared notebooks.
- Sidebar should be more condensed.
- Web clipper needs some work. Doesn't properly capture text on all sites.

#### [Day One](http://dayoneapp.com/)

Day One [supports Markdown](http://help.dayoneapp.com/tips-and-tutorials/markdown-guide).

#### [Dropbox Paper](https://www.dropbox.com/paper)

##### Dropbox Paper Pros

- Markdown export
- Collaboration
- Sync
- Embedding works well

##### Dropbox Paper Cons

- Paper files don't show up in your regular Dropbox file structure
- No tags
- No themes
- No internal linking
- Only has H1-H2. H3 shows up as bold when downloading Markdown files.
- PDFs embedded in Dropbox Paper documents don’t lead to the actual PDF when clicked, in the mobile apps.
- PDF thumbnails are too large when inserted as single PDFs. When two or more files are inserted, the thumbnails are next to each other and the size is more reasonable. Needs a "view as attachment" option like Evernote.

#### [iA Writer](https://ia.net/writer)

iA = information Architects

##### iA Writer pros

- Cross-platform
- Light/dark themes
- Currently just a one-time payment model, though that will probably change.

##### iA Writer cons

- Lacks some of the features of Bear
- No syntax highlighting
- Multimedia?

#### [Inkdrop](https://www.inkdrop.info/)

[Features](https://www.inkdrop.info/features): Markdown, themes, encryption, cross-platform. Seems to be like Bear, but cross-platform. Check out the developer's [Medium blog](https://blog.inkdrop.info).

#### [Jottings](http://jottingsapp.com/)

iOS note app with Markdown, tagging, and Dropbox sync.

#### [Laverna](https://laverna.cc/)

##### Laverna Pros

- Encrypted
- Markdown
- Multimedia
- Internal linking
- Make tags with #tag
- Open source
- Built with Electron

##### Laverna Cons

- Evernote import?
- No Android app yet
- No dark themes yet
- No Markdown TOC

#### [Simplenote](https://simplenote.com/)

From WordPress

##### Simplenote Pros

- Markdown support

##### Simplenote Cons

- Evernote import?
- Multimedia?

#### [Standard Notes](https://standardnotes.org/getting-started)

##### Standard Notes Pros

- Simple, dependable text note app
- Note tagging
- Themes like solarized and dark
- Extensions to add features like Markdown
- Encrypted
- Backup to Dropbox and Google Drive
- "Built to last"

##### Standard Notes Cons

- Extensions only work on desktop and web.
- Can't attach files from mobile devices.
- Not great with multimedia. Tried to drag and drop a movie, and it just displayed the movie instead of my notes.
- [Evernote import](https://standardnotes.org/evernote): Formatting, images, and attachments will not be copied over. Have to break up .enex into 250 MB segments.
  - My response to email survey:
    > *Have you ever tried Standard Notes Extended?*
    > No. If I became a regular user, I would happily pay for Extended. I'm not regularly using Standard Notes because I'm heavily invested in Evernote. I've been using it for six years, and have a 4 GB database with ~4400 tagged notes. I would love to migrate from Evernote to another service, converting from rich text to Markdown and encrypting my data, while keeping my multimedia attachments. Bear is one example of this type of migration, but I don't use Bear because it's Apple-only.

#### [Turtl](https://turtlapp.com/)

[Turtl blog on Tumblr](http://turtlapp.tumblr.com/)

##### Turtl Pros

- Promising encrypted Evernote alternative
- Evernote import coming in 0.6.5
- Markdown
- Sharing
- Some multimedia support
- Android app

##### Turtl Cons

- Still needs more development
- Not sure how dependable this app will be. The developers don't even own a MacBook.
- No dark themes yet

#### [Typora](https://typora.io/)

##### Typora Pros

- File list panel, allowing you to use any cloud service to sync.
- CSS configurable
- Support for images
- Document export
- Footnote feature is cool

##### Typora Cons

- Feature-poor
- Not for android
- If it’s not for mobile and not multimedia, what’s the point beyond Sublime Text? Or Dillinger?

#### [Ulysses](https://ulyssesapp.com/)

##### Ulysses Pros

- Nice interface
- Markdown
- Dark themes
- Can also manage journal articles and research

##### Ulysses Cons

- Apple only
- Encryption?
- Moved to expensive subscription model
- Maintains article tags as "keywords," a fatal flaw shared by other apps like [Papers](https://www.readcube.com/papers/).

### In-browser editors

- [Dillinger](https://dillinger.io/): In-browser Markdown editor with live preview.
- [GitBook](https://www.gitbook.com/): Online platform for writing documentation. It combines and converts Markdown files into multimedia-enabled notebooks, like book chapters.
- [Gnotes](https://notes.giggy.com/): Write Markdown, save to Dropbox, see in Evernote. One-way only.
- [Markdown Here](https://markdown-here.com/index.html): Allows Markdown formatting for in-browser web apps like Gmail. See [GitHub](https://github.com/adam-p/markdown-here).
- [Marxico](http://marxi.co/):
  - In-browser Markdown editor based on Dillinger.
  - Works with images.
  - Has live TOC.
  - Renders well on mobile browsers, but only selection capability available is "select all".
  - May not have seamless integration with Evernote. See [discussion on Evernote forums](https://discussion.evernote.com/topic/99861-native-markdown-support/?do=findComment&comment=448394).
- [StackEdit](https://stackedit.io/): In-browser Markdown editor with live preview. Uses PageDown, the engine powering the Markdown capabilities of the Stack Exchange forums.
- Udacity discussion forums: You can use Markdown formatting in your forum posts.

[(Back to top)](#top)

### Social apps

#### Gitter

[Gitter](https://gitter.im/) uses Markdown formatting for chats. See their [Markdown basics](https://gitter.zendesk.com/hc/en-us/articles/200176682-Markdown-basics) support article.

#### ~~Slack~~

Slack uses a simplified pseudo-Markdown and has [stated](https://get.slack.help/hc/en-us/articles/202288908#a-note-about-markdown) that it will not be building in full Markdown capabilities.

[(Back to top)](#top)