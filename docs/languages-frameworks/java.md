# Java

Before using the following tools, please make sure that you have:
- [Registered TrueAutomation.io account](https://app.trueautomation.io/auth/signup)
- [Installed TrueAutomation client](/getting-started/installation.md ':target=_blank')
- [Initialized project](/initializing/initializing-automatically.md ':target=_blank')

## RemoteWebDriver

TrueAutomation supports using [RemoteWebDriver](https://github.com/SeleniumHQ/selenium/wiki/RemoteWebDriver) with different Java-based technology stacks. To use RemoteWebDriver with TrueAutomation, set the following parameters into TrueAutomationDriver:
- remote address of a browser driver or WebDriver Server;
- desired capabilities;

```java
WebDriver driver = new TrueAutomationDriver(new URL("http://remote_address"), new DesiredCapabilities());
```
	
Here is the example of using RemoteWebDriver with TrueAutomation in Java:

```java
   import io.trueautomation.client.driver.TrueAutomationDriver;
   import org.openqa.selenium.By;
   import org.openqa.selenium.WebDriver;
   import org.openqa.selenium.remote.DesiredCapabilities;
   import org.testng.annotations.AfterTest;
   import org.testng.annotations.BeforeTest;
   import org.testng.annotations.Test;

   import java.net.MalformedURLException;
   import java.net.URL;
   import java.util.concurrent.TimeUnit;

   import static io.trueautomation.client.TrueAutomationHelper.ta;

   public class exampleTest {
       private WebDriver driver;
       private By loginBtn = By.cssSelector(ta("ta:mainPage:loginBtn", "a.login-btn"));
       private By signupBtn = By.cssSelector(ta("ta:mainPage:signupBtn", "div.sign-up-container > a"));
       private By emailFl = By.name(ta("ta:loginPage:email", "email"));

       @BeforeTest
       public void beforeTest() throws MalformedURLException {
           driver = new TrueAutomationDriver(new URL("http://remote_address"), new DesiredCapabilities());
           driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);
       }

       @Test
       public void exampleTest() {
           driver.get("https://trueautomation.io");

           driver.findElement(loginBtn).click();
           driver.findElement(signupBtn).click();

           driver.findElement(emailFl).sendKeys("your@mail.com");
       }

       @AfterTest
       public void afterTest() {
           driver.quit();
       }
   }
```

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-java-remoteWebDriver**

## GRID

TrueAutomation supports using [Selenium GRID](https://www.seleniumhq.org/docs/07_selenium_grid.jsp) in different Java-based technology stacks.

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

Here is the example of using GRID with TrueAutomation in Java:

```java
import io.trueautomation.client.driver.TrueAutomationDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.MutableCapabilities;
import org.openqa.selenium.chrome.ChromeOptions;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import java.net.MalformedURLException;
import java.net.URL;
import java.util.concurrent.TimeUnit;

import static io.trueautomation.client.TrueAutomationHelper.ta;

public class exampleTest {
    private TrueAutomationDriver driver;
    private By loginBtn = By.cssSelector(ta("ta:mainPage:loginBtn", "a.login-btn"));
    private By signupBtn = By.cssSelector(ta("ta:mainPage:signupBtn", "div.sign-up-container > a"));
    private By emailFl = By.name(ta("ta:loginPage:email", "email"));

    @BeforeTest
    public void beforeTest() throws MalformedURLException {
        driver = new TrueAutomationDriver(new URL("http://localhost:4444/wd/hub"), new ChromeOptions());
        driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);
    }

    @Test
    public void exampleTest() {
        driver.get("https://trueautomation.io");
        driver.findElement(loginBtn).click();
        driver.findElement(signupBtn).click();
        driver.findElement(emailFl).sendKeys("your@mail.com");
    }

    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```

To run your test file use the command below in your command line:

<!-- tabs:start -->
#### **Maven**
```bash
mvn -Dtest=yourTest test
```  

#### **Gradle**
```bash
gradle test --tests yourTest
```   
<!-- tabs:end -->

A new browser window will be opened, test actions will be performed. You’ll get the test info in your command line:

<!-- tabs:start -->
#### **Maven**
![Test output](../_images/java-grid-test.png 'Test output')

#### **Gradle**
![Test output](../_images/gradle-test.png 'Test output')
<!-- tabs:end -->

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-java-grid**

## Appium

TrueAutomation supports [Appium](https://appium.io/)

To get started, make you have Appium and all of its dependencies installed. If you do not have Appium in place, please refer to its documentation to install it.

Update your ‘pom.xml.’ file, which should contains this maven dependency:

```xml
<dependency>
    <groupId>io.appium</groupId>
    <artifactId>java-client</artifactId>
    <version>6.1.0</version>
</dependency>
```

Run Appium server, using Terminal, appium desktop app, [AppiumServiceBuilder](https://appium.github.io/java-client/io/appium/java_client/service/local/AppiumServiceBuilder.html) from `java-client`. By default Appium is run on port number `4723`.

Install url into TrueAutomationDriver, based on Appium hub, and all capabilities you need.

For example:

Set up driver for iOS (make sure that you use your device udid):

```java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "iPhone");
capabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME, "XCuiTest");
capabilities.setCapability(MobileCapabilityType.UDID, "101F5280-F668-4FDD-987F-3FAD33E028F8");
capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, "ios");
capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "safari");

WebDriver driver = new TrueAutomationDriver(new URL("http://localhost:4723/wd/hub"), capabilities);
```

Set up driver for Android (make sure that you use your device udid):

```java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "Android device");
capabilities.setCapability(MobileCapabilityType.UDID, "8618f72f53");
capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, "Android");
capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "chrome");

WebDriver driver = new TrueAutomationDriver(new URL("http://localhost:4723/wd/hub"), capabilities);
```

After all changes the test should look like:

```java
import io.appium.java_client.remote.MobileCapabilityType;
import io.trueautomation.client.driver.TrueAutomationDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.remote.RemoteWebDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import java.net.MalformedURLException;
import java.net.URL;
import java.util.concurrent.TimeUnit;

import static io.trueautomation.client.TrueAutomationHelper.ta;

public class exampleTest {
    private WebDriver driver;
    private By loginBtn = By.cssSelector(ta("ta:mainPage:loginBtn", "a.login-btn"));
    private By signupBtn = By.cssSelector(ta("ta:mainPage:signupBtn", "div.sign-up-container > a"));
    private By emailFl = By.name(ta("ta:loginPage:email", "email"));

    @BeforeTest
    public void beforeTest() throws MalformedURLException {
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "<DEVICE_NAME>");
        capabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME, "<AUTOMATION_NAME>");
        capabilities.setCapability(MobileCapabilityType.UDID, "<DEVICE UDID>");
        capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, "<PLATFORM_NAME>");
        capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "<BROWSER_NAME>");
        driver = new TrueAutomationDriver(new URL("http://localhost:4723/wd/hub"), capabilities);

        driver.manage().timeouts().implicitlyWait(15, TimeUnit.SECONDS);
    }

    @Test
    public void exampleTest() throws InterruptedException {
        driver.get("https://trueautomation.io");

        driver.findElement(loginBtn).click();
        driver.findElement(signupBtn).click();
        driver.findElement(emailFl).sendKeys("your@mail.com");
    }

    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```

Before you run the test, make sure that you have updated DesireCapabilities(`DEVICE_NAME`, `AUTOMATION_NAME`, `UDID`, `PLATFORM_NAME`, `BROWSER_NAME`) according to the capabilities of the device that is used for running the test.

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-java-remoteWebDriver**

## PageFactory

TrueAutomation supports [PageFactory](https://github.com/SeleniumHQ/selenium/wiki/PageFactory). Instead of the annotation `@FindBy()`, use this one `@FindByTA()`.

Insert the following line to make the annotation available:

```java
import io.trueautomation.client.driver.FindByTA;
```

The `@FindByTA` annotation supports all the locators strategies such as `id`, `className`, `css`, `xpath`, `tagName`, `linkText`, `partialLinkText`, and TrueAutomation locator strategy - `taName`.

For example: 

```java
@FindByTA(taName="mySite:loginPage:username", id = "username") 
private WebElement userName;

// or

@FindByTA(taName="mySite:loginPage:username", how = How.ID, using = "username") 
private WebElement userName;
```

If you already have the element `mySite:loginPage:username` in the object repository of your cloud project, you can use only the `taName`.

```java
@FindByTA(taName="mySite:loginPage:username") 
private WebElement userName;
```

Here is the example of the test, using PageFactory:

```java
import io.trueautomation.client.driver.FindByTA;
import io.trueautomation.client.driver.TrueAutomationDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.PageFactory;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import java.util.concurrent.TimeUnit;

import static io.trueautomation.client.TrueAutomationHelper.ta;

public class exampleTest {
    private WebDriver driver;

    @FindByTA(taName = "ta:mainPage:loginBtn", css = "a.login-btn")
    private WebElement login;

    @FindByTA(taName = "ta:mainPage:signupBtn", css = "div.sign-up-container > a")
    private WebElement signup;

    @FindByTA(taName = "ta:loginPage:email", name = "email")
    private WebElement emailField;

    @BeforeTest
    public void beforeTest() {
        driver = new TrueAutomationDriver();
        driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);

        PageFactory.initElements(driver, this);
    }

    @Test
    public void exampleTest() {
        driver.get("https://trueautomation.io");

        login.click();
        signup.click();

        emailField.sendKeys("your@mail.com");
    }

    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```

Once the test runs successfully for the 1st time and all the elements are saved into the objects repository, you can use just `taName`.

![Object repository with elements](../_images/cloud-objects.png 'Object repository with elements')
 
The test will look like this:
 
```java
import io.trueautomation.client.driver.FindByTA;
import io.trueautomation.client.driver.TrueAutomationDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.PageFactory;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import java.util.concurrent.TimeUnit;

import static io.trueautomation.client.TrueAutomationHelper.ta;

public class exampleTest {
    private WebDriver driver;

    @FindByTA(taName = "ta:mainPage:loginBtn")
    private WebElement login;

    @FindByTA(taName = "ta:mainPage:signupBtn")
    private WebElement signup;

    @FindByTA(taName = "ta:loginPage:email")
    private WebElement emailField;

    @BeforeTest
    public void beforeTest() {
        driver = new TrueAutomationDriver();
        driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);

        PageFactory.initElements(driver, this);
    }

    @Test
    public void exampleTest() {
        driver.get("https://trueautomation.io");

        login.click();
        signup.click();

        emailField.sendKeys("your@mail.com");
    }

    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-pageFactory**

<br>

# TrueAutomation capabilities

TrueAutomation supports all WebDriver capabilities and expands them with our internal capabilities.

#### TrueAutomation embedded drivers selection

There are internal capabilities for embedded drivers selection through the Desired Capabilities. These are special key and value pairs that are sent to the server in the JSON object when requesting a new automation session. They specify driver and its version that should be used in a test.

|**Key**| &nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp;**Type**&nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp; | **Description**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;     |
|:---:|:---:|:---|
|driver| string | The driver name being used. Should be one of: <br>- chromedriver<br>- geckodriver<br>- microsoftwebdriver<br>- safaridriver|
|driver_version| string | The driver version being used. If driver version is <br>not set, the test will be run with the latest driver <br>version.<br>|

**Example of using**

```java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability("driver", "geckodriver");
capabilities.setCapability("driver_version", "0.22.0");

driver = new TrueAutomationDriver(capabilities);
```

You can observe a list of current drivers and their versions using the `trueautomation driver list` command.
