# Element picker #

TrueAutomation Element Picker is a web browser extension, that gives you an easy, intuitive and fast way of creating Smart Locators that should be used in a test.
Literally, all you need to do is pick elements that you need and project that they belong to - the elements will be ‘inspected’ by TrueAutomation AI, 
smart-locators will be generated and added to your project objects repository automatically. You can use those Smart locators in your test code directly from IDE.
    
> You can download [TrueAutomation browser extension](https://chrome.google.com/webstore/detail/trueautomationio-element/khpnbhifngechnmadjdgddjjaiioncoh) from Chrome Web Store

### Use TrueAutomation element picker to: ###

- create tests faster in multiple times    
- eliminate elements inspection from your workflow    
- give locators human-readable names (by using [TrueAutomation naming patterns](/getting-started/ta-locators))    
- create tests in cases when it’s impossible to use `IDs`, `names`, `XPath` or some other locator
- minimize tests maintenance (and if such is needed, update locators with a click)

### Currently supporting: ###

- Chrome Browser (both desktop and mobile view)

## Initial setup ###

Install [TrueAutomation Chrome extension](https://chrome.google.com/webstore/detail/trueautomationio-element/khpnbhifngechnmadjdgddjjaiioncoh) for picking web elements

## How to use TrueAutomation element picker ###

1. Open your terminal and run the command `trueautomation ide`<br/>
If you do not run this command, TrueAutomation Chrome extension will return an error.
![IDE not started](../_images/ide-not-started.png  'TrueAutomation IDE has not been started')

2. Go to the website or web application that you need to cover with tests and activate extension
![Activate TrueAutomation extension](../_images/activate-extension.png  'Activate TrueAutomation extension')

3. Select a project (that you have in your [TrueAutomation.io cloud account](https://app.trueautomation.io/)) where the Smart locators should belong.<br/>
In case you do not have a project - make sure to create one.
![Select a project](../_images/select-project.png  'Select a project')
![TrueAutomation.io cloud account](../_images/cloud-project-list.png  'TrueAutomation.io cloud account')
Once the project is selected, for the elements, that you pick a Smart Locator will be generated and added to project objects repository

4. In order to add a new Smart locator to objects repository, push ‘Select an Element’ button.<br/>
An element will be inspected by TrueAutomation AI, a Smart-locator will be generated automatically and added to current project objects repository.
![Select an element](../_images/select-element-btn.png  'Select an element')
click on the element, located on the current web page.
![Element on page](../_images/element-on-page.png  'Element on page')
Once you’ve clicked on the element, it will be selected and you will be asked to give it a name: **"ENTER A SELECTED ELEMENT NAME"**
> Give it a name (e.g.: `ta:homePage:emailFl`) and click ‘Save’ button 
>
We recommend to use namespaced syntax to make sure you always have human-readable names that make sense. You can learn more [here]().
![Element name](../_images/name-element.png  'Element name')<br/>
Once the element is detected and recorded by TrueAutomation - you will get a confirmation popup. This means a Smart-locator has been generated and added to objects repository successfully. You can use it now in your test code.
<!--If you use .gif do new line before-->
>
![Add element using Element Picker](../_gif/add-new-element20fps.gif  'Add element using Element Picker')
To view the list of all Smart-locators, that have been created for current project, go to your [TrueAutomation.IO cloud account](https://app.trueautomation.io/), open the particular project and click ‘View elements’ button.
![Element tree](../_images/element-tree.png  'Element tree')

5. In order to rewrite/update an existing element, enter the name of that element into the field on the right, next to "Select an Element" button.<br/>
If the element exists, "Select an Element" button will change its name to "Reselect an Element".
> Hit the "Reselect an Element" button and click on any element located on the web page, to rewrite or update the current one.
>
![Reselect element](../_images/reselect-element.png  'Reselect element')
Once done, a confirmation popup will be displayed.
>
![Reselect element using Element Picker](../_gif/reselect-element20fps.gif  'Reselect element using Element Picker')

6. In order to switch to Mobile View of the website, click ‘Mobile’ button.
![Switch to mobile](../_images/mobile-btn.png  'Switch to mobile')
The current webpage will be displayed in mobile view. In order to go back to desktop view, hit the same button once again.
![Mobile view](../_images/mobile-view.png  'Mobile view')