# Troubleshooting

### Atom plugin does not start automatically on Windows

TrueAutomation Atom plugin does not start automatically on Windows when user opens TrueAutomation project.
**Workaround:** run command `trueautomation ide` from root folder of your project. It will launch TrueAutomation Atom plugin.

### Atom plugin can't manage browser window on Linux and Windows

After clicking on the TA button in Atom, the browser will not open automatically. You need to open a new Chrome browser window or tab, go to the website that should be tested, activate the Element Picker Chrome extension and select the element. Here is the link on [how to use Element Picker](https://app.trueautomation.io/howtouse/)

### Running tests in Internet Explorer 11

There is a problem with Selenium "IEDriverServer" both embedded and remote. Driver session is not created due to the lack the necessary capabilities, although the capabilities transmitted.

![Technology stack](../_images/troubleshooting-IEDriverServer.png 'Technology stack')

We are sorry for the inconvenience. The problem will be solved in the near time.

### Microsoft WebDriver version

Such issue can occur if you run tests using the wrong driver version:

![Technology stack](../_images/troubleshooting-MicrosoftWD.png 'Technology stack')

Microsoft WebDriver version should be the same as the Microsoft Edge browser version.