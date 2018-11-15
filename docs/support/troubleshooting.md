# Troubleshooting

### Atom plugin does not start automatically on Windows

TrueAutomation Atom plugin does not start automatically on Windows when user open trueautomation project.
**Workaround:** run command `trueautomation ide` from root folder of your project. It will launch TrueAutomation Atom plugin.

### Atom plugin can't manage browser window on Linux and Windows

After clicking on the TA button in Atom, the browser will not open automatically. You need to open a new window or chrome browser tab, go to the link to the site that you need to test, activate the Element Picker chrome extension and select the element. Here is the link [how to use Element Picker](https://app.trueautomation.io/howtouse/)

### Running tests in Internet Explorer 11

Now, there is a problem of using "IEDriverServer" both embedded and remote. In particular, the driver session is not created due to the lack the necessary capabilities, although it is transmitted.

![Technology stack](../_images/troubleshooting-IEDriverServer.png 'Technology stack')

We are sorry for the inconvenience. The problem will be solved in the near time.


### Microsoft WebDriver version

The next problem can appear during running tests if you use the wrong driver version:

![Technology stack](../_images/troubleshooting-MicrosoftWD.png 'Technology stack')

Microsoft WebDriver version should be the same as the Microsoft Edge browser version.