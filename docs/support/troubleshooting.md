# Troubleshooting

### Running tests in Internet Explorer 11

Now, there is a problem of using "IEDriverServer" both embedded and remote. In particular, the driver session is not created due to the lack the necessary capabilities, although it is transmitted.

![Technology stack](../_images/troubleshooting-IEDriverServer.png 'Technology stack')

We are sorry for the inconvenience. The problem will be solved in the near time.


### Microsoft WebDriver version

The next problem can appear during running tests if you use the wrong driver version:

![Technology stack](../_images/troubleshooting-MicrosoftWD.png 'Technology stack')

Microsoft WebDriver version should be the same as the Microsoft Edge browser version.