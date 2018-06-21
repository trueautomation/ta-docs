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

## PageObject & PageFactory

Check out an example of the test project, using PageObject & PageFactory, here: https://github.com/shapovalovei/trueautomation-testng