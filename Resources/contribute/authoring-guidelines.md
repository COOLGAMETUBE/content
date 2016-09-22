# Authoring guidelines and best practices

## Guidelines

When creating a new topic, or updating an exisitng one, there are a handful of things to keep in mind.

1. **Creating a new topic:**

  When creating new content, please start with the following templates (view in *Raw* mode):

  * [Sample template](template/sample-template.md)
  * [Documentation template](template/docs-template.md)
  
  **Be sure to add** your file to the correct index file:
  
  * Samples add to [_samples.json](/_data/_samples.json)
  * Docs add to [_docs-index.json](/_data/_docs-index.json)

2. **Save your files in the following directories**

  * Images: `content/Resources/images/<folder name>/<your filename>`
  * Documentation: `content/en-US/Docs`
  * Samples: `content/en-US/Samples`

  Please use upper camel case (e.g. BackgroundColor) when naming your files. 

  Try to be as descriptive as possible without making your titles too long (good descriptions makes everyone's life easier) 

  For an image naming example, there is a "Noobs" folder for all the images used in the Noobs topics - it spans multiple articles but has a consolidated use.  If there isn't a folder that fits what your images are for, please create a new folder for your images.

3. **Writing in markdown**

  For manageability and consistent look and feel, we enforce that our docs and samples be written in [Markdown](https://daringfireball.net/projects/markdown/basics). Complex formatting can be done with Liquid templates - details on those below.
   
  We will make exceptions to use html if needed.
  
  Good examples:

  * Docs: `content/en-us/docs/PowerShell.md` 
  * Samples: `content/en-us/samples/helloworld.md`

4. **Misc guidelines**

  * Use only one H1 (#) per topic
    * Very important for SEO
  * H1 and title (in the metadata) should be the same
    * (e.g. title: AllJoyn and # AllJoyn)
  * Fill out metadata
    * At the top of each file, you'll see a section starting and ending with "---" where metadata for that topic lives.  Fill this section with information pertaining to the topic you're working on.

## Best Practices

### Renaming or moving files, how to redirect pages
If you need to move or rename a file (or more specifically, the permalink - however the filename and permalink should always match) please follow these steps:

1. Create new file at desired location, and copy all content in (be sure to update permalink etc. to what you want it to be).
2. Leave the existing file in it's old location, with the old permalink
3. Change the layout to "redirect" and delete all content under the metadata (section contained in ---) and place the following code in:

  {% include redirect.html url="/windows/iot/<newURL>.htm" %}
  
  This will create a client side redirect to the new page for any external links or bookmarks our users have

4. Search the entire repo for references to the old page, and update those to the new page
5. Submit a single PR that contains all of the above changes together
6. Once that is all done, email the Halcyon owners (Ivor and Stephen) a mapping of the old urls to the new urls, so we can put a permanent server redirect in place to clean up search results.

  For an example, look under en-US/win10/Docs.md

### Do not check in binaries
Once a binary is added to the repository, it will be there forever.

Please do not add binaries to Git including:
* The output from a build (debug/release)
* SDF file (code database)
* Nuget package directories

Acceptable binaries:
* PNG, JPG, or other image formats

### Liquid templates and common files

Our build system supports liquid templates (those sections with the % signs in them).  This allows us to include commonly used snippets or insert a bit of html without needing to write it in manually.  The plus side is it allows us to use common things (think nice looking grid layouts or tables) or include a common sample in several different docs without copy/pasting.

These templates need to live within the _includes folder in the root, and are referenced by `{% include redirect.html url="http://www.microsoft.com" %}` which will insert whatever that file is at this point in your article.  You can add arguments or content to the include call. 

Examples on usage of [liquid basics](https://help.shopify.com/themes/liquid/basics) and the [liquid cheatsheet](http://cheat.markdunkley.com/) are a few pages that I find useful to learn about Liquid.

### Writing

There is much more that goes into a well written article than you'd think! Below are some suggestions of things to consider when proofreading your article.

**Voice**

Voice is, simply put, your writing style in terms of syntax, verbage, verbosity etc. When we're writing for the users of Windows IoT, we always try to present our information in a relatively unified voice. Try to keep the following in mind:

* **Write in a supportive and informative way.** Try not to write in a way that could be interpreted as condescending - no one wants to feel belittled (even if unintentionally) when they're trying to learn something new.
* **Elaborate on any non-obvious point.** Make sure you explain anything that some of your audience might not understand. It is much better to over explain something and let those who know it skim over it. We want everyone to feel included when using IoT Core.
* **Maintain a single tense**. Usually we prefer present tense - this is rarely a concern in our docs.
* **Keep a clear logical flow through your article.** If you must reference something that you don't explain until later, mention so. Lists are helpful to keep your article flow in line.
* **Be as direct as possible.** Shorter, more direct sentences are the best. Give all the information the user needs, but try not to cover more than is needed to achieve their task. If needed, provide a link to a related topic and let the audience decide if they want to read about the other topic.
* **Proof read.** Take a quick break from writing and review it with fresh eyes. You may find obvious mistakes that were not so obvious before.

**Title and headings** 

* Title and headings are **all sentence-case** (only first word and proper nouns capitalized).
* The **title should be an H1 (#)**. Only one H1 per topic.
* The **next level of headings should be H2 (##)**, and so forth. Don't skip heading levels.
* Avoid H4s, H5s, etc.

**Numbered lists and bulleted lists**

* **Use numbers to indicate steps** that go in a specific order (markdown = 1. Item, 2. Item).
* **Use bullets for lists** of unordered items (markdown = * item, or - item).
* **Use paragraphs** (no bullets or numbers) for text that’s not in a list.

**Terminology and abbreviations**
* **Use the same term throughout your doc**. Don't go back and forth between terms (such as “machine” and "computer" and "PC") when you are referring to the same thing. We have decided on the following terms: "Device" (referring to the Raspberry Pi board), "Peripheral" (for anything hooked up to the device/Raspberry Pi), and "PC" (referring to the computer). 
* **Do not abbreviate PowerShell** to PS unless it's part of a command. On first mention, use Windows PowerShell.
* **Do not abbreviate product names** unless there is a legally-approved acronym. *Official name of the Redstone 1 update to Windows 10: "Windows 10, version 1607". 
* **Spell out acronyms on first mention**, and include the acronym in parentheses. Thereafter, you can use the acronym by itself. 
**Example** – first mention: class identifier (CLSID); second mention: CLSID

**Formatting**
* **Use bold for UI entries**. (markdown = `**term**`)
Example: To start PowerShell as an administrator, right-click **Windows PowerShell**, and then select **Run as administrator**.
* **To emphasize a word, use italics**, not bold. (markdown = `*term*`)
* **For notes**, use the following liquid template: `{% include note.html text="This is a note" %}`
  * The same thing can be done with `tip.html`, and `warning.html`

**Links and cross-references**
* When you add a cross-reference, use this syntax: **For more information about X, see Y.**
Example: For a list of commands and utilities that you can use with PowerShell, see the [Command Line Utils]() page.
* **Format links** using the display name, not the URL, between the brackets: `[Display Name](URL)`.
* **Do not say, “Click here” or “Go here.”** Use the title of the page you’re pointing to.
* **Remove "en-us"** from TechNet and MSDN URLs (try them first). 
* **Add a "Related topics"** section (for topics in your repo) or "See also" or "Additional resources" section (for topics outside your repo) at the end of the page that at a minimum links back to your parent topic (to help users navigate).

**Images**
* **Resize your images** if they appear too big on stage or live.
* **Limit the number of your images** to only those you absolutely need to guide the user. Each image adds to page load time.

For more information, see the Windows Open Publishing Guide at http://aka.ms/windows-op-guide.



### References

1. [GitHub Documentation](https://help.github.com/)
2. [Git Cheatsheet!](https://github.com/github/training-materials/blob/master/downloads/github-git-cheat-sheet.pdf?raw=true)
3. [Git Documentation](http://www.git-scm.com/book/en/)

___

### How to contribute

1. [Get set up](get-setup.md)
2. [Making changes](making-changes.md) 
3. **[Authoring guidelines and best practices](authoring-guidelines.md)**

