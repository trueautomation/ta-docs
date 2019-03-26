# Human-readable names

One of the most unpleasant things, related to regular locators is their names. They often do not make any sense, do not give an idea to which element they are tied to and are hard to read.
Since TrueAutomation Smart-locators are not tied to specific XPathes, IDs and class names you can give human-readable names that you prefer to your Smart-locators.

We’ve gone one step further and introduced a naming pattern that makes it easier to navigate among locators and organize them based on the place where they belong on the page.

You can give names that consists of words, separated with `:` E.g.:

`pageName:elementName`
<br>
`pageName:widgetName:elementName`
<br>
`siteName:pageName:widgetName:elementName`
<br>
The number of blocks separated with a ‘colon’ is not limited, you can use as many as you want.

?> However we do not recommend to use too long names. The shorter the name the easier it is to read and use it in test code.

In your Objects Repository Smart-locators with human-readable names are organized in a tree-like structure and are sorted based on the name of the blocks, used in a name. E.g.
All Smart locators that belong to `homePage` will be organized under `homePage` category in the project they belong to in your Objects Repository.

?> Every Smart-locator, that has been added using Element Picker will also have an element screenshot. Locators, that have been added using initial locators will not have element screenshots attached.

Here’s an example.

Let’s say we have created a number of Smart-locators using Chrome element picker and have named them:
* `homePage:emailFl`
* `homePage:goBtn`
* `homePage:loginBtn`
* `homePage:docsLink`

Here is how these smart locators will be displayed in the Objects Repository:

![Human-readable names](../_images/human-names.png 'Human-readable names')

#### Actions you can apply to Smart-locators in objects repository:

**1. Copy the full name of your Smart-locator to use it in your IDE.**

Click on the locator name (e.g. `emailFl`), the full name `homePage:emailFl` will be automatically copied and can be pasted into the test code in your IDE.

![Copy name](../_gif/copy-name-from-cloud.gif 'Copy name')

**2. View element screenshot.**

A thumbnail of the element screenshot is displayed next to each smart locator. Hover the cursor over the thumbnail to make it bigger.

![Zoom screenshot](../_gif/zoom-screenshot.gif 'Zoom screenshot')

**3. Delete single Smart-locator**

![Delete single Smart-locator](../_gif/delete-single.gif 'Delete single Smart-locator')

**4. Delete all Smart-locators**

![Delete all Smart-locators](../_gif/delete-all.gif 'Delete all Smart-locators')
