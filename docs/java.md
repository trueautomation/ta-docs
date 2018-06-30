# Java
## RemoteWebDriver
TrueAutomation supports [RemoteWebDriver](https://github.com/SeleniumHQ/selenium/wiki/RemoteWebDriver). To use it, set the following parameters into TrueAutomationDriver:
- remote address of web driver or hub as url objects;
- capabilities.

```java
WebDriver driver = new TrueAutomationDriver(new URL("http://<driver_host>:<driver_port>"), new DesiredCapabilities());
```
	
Here is the example of the test, using RemoteWebDriver: 
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
       private By loginBtn = By.cssSelector(ta("loginBtn", "a.login-btn"));
       private By signupBtn = By.cssSelector(ta("signupBtn", "div.sign-up-container > a"));
       private By emailFl = By.name(ta("emailFl", "email"));

       @BeforeTest
       public void beforeTest() throws MalformedURLException {
           driver = new TrueAutomationDriver(new URL("http://<driver_host>:<driver_port>"), new DesiredCapabilities());
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


## Appium
TrueAutomation supports [Appium](https://appium.io/).
Ensure you have Appium and all of Appium's dependencies installed If you don’t have, use the Appium documentation to install it.

Update your ‘pom.xml.’ file, which should look like this:
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>appium-java</groupId>
  <artifactId>appium-java</artifactId>
  <version>1.0</version>
  <properties>
    <maven.compiler.source>1.6</maven.compiler.source>
    <maven.compiler.target>1.6</maven.compiler.target>
  </properties>
  <dependencies>
    <dependency>
      <groupId>org.seleniumhq.selenium</groupId>
      <artifactId>selenium-java</artifactId>
      <version>3.11.0</version>
    </dependency>
    <dependency>
      <groupId>org.testng</groupId>
      <artifactId>testng</artifactId>
      <version>6.10</version>
      <scope>exampleTest</scope>
    </dependency>
    <dependency>
      <groupId>io.trueautomation</groupId>
      <artifactId>trueautomation-client</artifactId>
      <version>0.3.3</version>
    </dependency>
    <dependency>
      <groupId>io.appium</groupId>
      <artifactId>java-client</artifactId>
      <version>5.0.0</version>
    </dependency>
  </dependencies>
  <repositories>
    <repository>
      <id>trueautomation-io</id>
      <name>TrueAutomation.IO MVN Repository</name>
      <url>https://mvn.trueautomation.io/artifactory/trueautomation</url>
    </repository>
  </repositories>
</project>
```

Run Appium server, using Terminal, appium desktop app, [AppiumServiceBuilder](https://appium.github.io/java-client/io/appium/java_client/service/local/AppiumServiceBuilder.html) from `java-client`

Install url into TrueAutomationDriver, based on Appium hub, and all capabilities you need.
For example:
```java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "iPhone X");
capabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME, "XCuiTest");
capabilities.setCapability(MobileCapabilityType.UDID, "101F5280-F668-4FDD-987F-3FAD33E028F8");
capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, "ios");
capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "safari");

WebDriver driver = new TrueAutomationDriver(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);
```

After all changes the text should look like:

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
        driver = new TrueAutomationDriver(new URL("http://<appium_host>/wd/hub"), capabilities);

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

Before you run the test, make sure that you have updated DesireCapabilities(`DEVICE_NAME`, `AUTOMATION_NAME`, `UDID`, `PLATFORM_NAME`, `BROWSER_NAME`)  according to the capabilities to the device, used for running the test.

Check out an example of an actual test here: https://github.com/shapovalovei/appium-testng-trueautomation

## PageFactory

TrueAutomation supports [PageFactory](https://github.com/SeleniumHQ/selenium/wiki/PageFactory). Instead of the annotation `@FindBy()`, use this one `@FindByTA()`.

Thus, place the following line to make the annotation available:

```java
import io.trueautomation.client.driver.FindByTA;
```

The `@FindByTA` annotation supports all the locators strategies such as `id`, `className`, `css`, `xpath`, `tagName`, `linkText`, `partialLinkText`, and TrueAutomation locator strategy - `taName`.

For example: 
```java
@FindByTA(taName="mySite:loginPage:username", id = "username") 
private WebElement userName;

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

As a test will have run successfully for the first time, and all elements will have been saved in the object repository, you can use just `taName`.

 ![Object repository with elements](_images/rep-with-elements.png 'Object repository with elements')
 
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

