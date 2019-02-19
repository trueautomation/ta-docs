# Atom IDE with Element picker 

TrueAutomation Element picker is a combination of IDE plugin and web browser extension that allow you to pick an element on the web page for which a unique "smart locator" is generated and used in your test code in IDE.
- IDE plugin integrates a TA button into your code. Once clicked a new browser session is initiated.
- Browser extension integrates with your browser. Once a new session is initiated by IDE plugin you will be able to pick an element that should be used in your test.

### Use TrueAutomation element picker to:

- create tests faster
- create tests in cases when it’s impossible to use `IDs`, `names`, `XPath` or some other locator
- maintain TrueAutomation-based tests faster

### Currently supporting:

- Atom IDE
- Chrome Browser

## Initial setup {docsify-ignore}

1. Install Atom IDE [atom.io](https://atom.io)
2. Install [TrueAutomation plugin for Atom](https://atom.io/packages/trueautomation-element-picker) (Atom package)
3. Install [TrueAutomation Chrome extension](https://chrome.google.com/webstore/detail/trueautomationio-element/khpnbhifngechnmadjdgddjjaiioncoh) for picking web elements

## How to use Atom IDE with TrueAutomation element picker {docsify-ignore}

1. Open or create a TrueAutomation-based project in Atom.<br/>
If the project is TrueAutomation-based, we will define that and automatically start the TrueAutomation Element picker. You will be informed about that.
>
<!--If you use .gif do new line before-->
![Picker](../_gif/picker-starting-notice.gif 'Picker starting notice')
Also, the special TA buttons will be added to your code only in places where just TA locators are used. TA button will not be displayed in cases where you use TA locator + Regular locator or just Regular locator (IDs, names, XPath, etc)

<!-- tabs:start -->
#### ** Java **
![Picker](../_images/taButton-java.png 'TA button')
#### ** Capybara **
![Picker](../_images/taButton-capybara.png 'TA button')
#### ** WebDriverIO **
![Picker](../_images/taButton-webdriverio.png 'TA button')
<!-- tabs:end -->

[See examples when (only) TA locators are used in code](/getting-started/ta-locators?id=example)

2. Click on the orange TA button in your code. Once you click, a new browser session will be initiated and you will have to pick the element, corresponding to a locator in your code.<br/>
> The same browser session will be used for elements picking until you close the browser window or close your project.

3. Go to the website or web application that you need to cover with tests

4. Select an element, that needs to be used in test. Click on the TA extension icon to activate it. Push ‘Select an Element’ button. Left-click on the element.
![Picker](../_images/select-element-atom.png 'Element Selection')
**Once the element is detected and recorded by TrueAutomation, a confirmation popup will be displayed. Now go back to your code, you will see that the recorded TA locator color is changed from red to green.**

<!-- tabs:start -->
#### ** Java **
![Picker](../_images/taLocatorColor-java.png 'TA locator')
#### ** Capybara **
![Picker](../_images/taLocatorColor-capybara.png 'TA locator')
#### ** WebDriverIO **
![Picker](../_images/taLocatorColor-webdriverio.png 'TA locator')
<!-- tabs:end -->

If you go to your TrueAutomation account, you will see that the recorded elements are added to the object repository.

![Picker](../_images/element-tree.png 'Element In Cloud')
