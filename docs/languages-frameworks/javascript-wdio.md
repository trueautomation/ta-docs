# JavaScript/WebdriverIO

Before using the following tools, please make sure that you have:
- [Registered TrueAutomation.io account](https://app.trueautomation.io/auth/signup)
- [Installed TrueAutomation client](/getting-started/installation.md ':target=_blank')
- [Initialized project](/initializing/initializing-automatically.md ':target=_blank')

## RemoteWebDriver

TrueAutomation supports using [RemoteWebDriver](https://github.com/SeleniumHQ/selenium/wiki/RemoteWebDriver) in the JavaScript/WebdriverIO technology stack. To use RemoteWebDriver with TrueAutomation, set the following parameters into `wdio.conf.js` file:
- remote address of a browser driver or WebDriver Server;
- the `remote` option;

```js
// wdio.conf.js
exports.config = {
    // ...
    services: ['trueautomation'],
    hostname: '127.0.0.1',
    port: 4444,
    path: '/',
    remote: true
    // ...
}
```

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-wdioV5-remoteWebDriver**

## GRID

TrueAutomation supports using [Selenium GRID](https://www.seleniumhq.org/docs/07_selenium_grid.jsp) in the JavaScript/WebdriverIO technology stack.

To get started, make sure to download Selenium Standalone Server from [here](https://docs.seleniumhq.org/download/) into the folder with your project.

![Selenium standalone server](../_images/seleniumStandaloneServer.png 'Test output')

In a separate command line window, navigate to the directory, where the `selenium-server-standalone` file  is located (this is the project's root folder) and run the command below to launch grid hub:    

```bash
java -jar selenium-server-standalone-3.14.0.jar -role hub
```

![Hub start](../_images/hub_start.png 'Test output')

In a separate command line window, navigate to the directory, where the `selenium-server-standalone` file  is located (this is the project's root folder) and run the command below to launch grid node:

```bash
java -jar selenium-server-standalone-3.14.0.jar -role node -hub http://localhost:4444/grid/register
```

![Node start](../_images/node_start.png 'Test output')

You will also need a driver for the browser where you want to execute your tests. This driver is used by WebDriver Server to start a browser of your choice. So make sure that one of the following conditions is met:

- A browser driver binary is in the system path;
- The WebDriver Server (node) was started with path to your browser driver:

```bash
-Dwebdriver.chrome.driver=path/to/your/chromedriver
```

- A browser driver is in the same directory as the `selenium-server-standalone` file;

> Please refer to [Selenium Grid documentation](https://github.com/SeleniumHQ/selenium/wiki/Grid2) for details on configuring your hub and nodes.

Here is the example of the `wdio.conf.js` file for using GRID with TrueAutomation in this technology stack:

```js
exports.config = {
    runner: 'local',
    specs: [
        './test/specs/**/*.js'
    ],
    maxInstances: 1,
    capabilities: [{
        maxInstances: 1,
        browserName: 'chrome'
    }],
    logLevel: 'error',
    deprecationWarnings: true,
    bail: 0,
    baseUrl: 'http://localhost',
    waitforTimeout: 10000,
    connectionRetryTimeout: 90000,
    connectionRetryCount: 3,
    services: ['trueautomation'],
    hostname: '127.0.0.1',
    port: 4444,
    path: '/wd/hub',
    remote: true,
    framework: 'mocha',
    mochaOpts: {
        ui: 'bdd',
        timeout: 60000
    }
}
```

Run `npm install` and then `npm test` commands to launch the test. A new browser window will be opened, test actions will be performed. You’ll get the test info in your command line:

![Test output](../_images/wdio-test.png 'Test output')

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-wdioV5-grid**

<br>

# TrueAutomation options

TrueAutomation supports all WebDriver capabilities implemented in the WebdriverIO through various options. We also support the additional features of WebdriverIO and expand them with our internal options.

#### TrueAutomation embedded drivers selection

TrueAutomation has special options for embedded drivers selection. These are special key and value pairs that are sent to the server when requesting a new automation session. They specify driver and its version that should be used in a test.

|**Key**| &nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp;**Type**&nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp; | **Description**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;|
|:---:|:---:|:---|
|driver| string | The driver name being used. Should be one of: <br>- chromedriver<br>- geckodriver<br>- microsoftwebdriver<br>- safaridriver|
|driverVersion| string | The driver version being used. If driver version is <br>not set, the test will be run with the latest driver <br>version.<br>|

**Example of using**

```js
// wdio.conf.js
exports.config = {
    // ...
    driver: 'geckodriver',
    driverVersion: '0.24.0'
    // ...
}
```

You can observe a list of current drivers and their versions using the `trueautomation driver list` command.

#### TrueAutomation logs

|**Key**| &nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp;**Type**&nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp; | **Description**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;|
|:---:|:---:|:---|
|trueautomationLog| string | The path to logfile. If the parameter is not set, <br>the TrueAutomation logfile will be saved to the `log` directory <br>in the format `trueautomation-${Date.now()}.log`.|

**Example of using**

```js
// wdio.conf.js
exports.config = {
    // ...
    trueautomationLog: 'log/trueautomation-${Date.now()}.log'
    // ...
}
```
