# Creating your first test in TrueAutomation using Java/Maven + GRID
1. Initialize TrueAutomation project on your machine in the preferred folder. (for details checkout the [initializing guide](/initializing/initializing-automatically.md))

2. Download the Selenium Standalone Server from [here](https://docs.seleniumhq.org/download/) to folder with your project
    ![Selenium standalone server](_images/seleniumStandaloneServer.png 'Test output')
3. Launch grid hub
    ```
    java -jar selenium-server-standalone-3.13.0.jar -role hub
    ```
    ![Hub start](_images/hub_start.png 'Test output')
4. Launch grid node
    ```
    java -jar selenium-server-standalone-3.13.0.jar -role node -hub http://localhost:4444/grid/register -port 5556
    ```
    ![Node start](_images/node_start.png 'Test output')

5. Change exampleTest.java with:

      ```java
         import io.trueautomation.client.driver.TrueAutomationDriver;
         import org.openqa.selenium.By;
         import org.openqa.selenium.Platform;
         import org.openqa.selenium.remote.DesiredCapabilities;
         import org.testng.annotations.AfterTest;
         import org.testng.annotations.BeforeTest;
         import org.testng.annotations.Test;
         
         import java.util.concurrent.TimeUnit;
         
         import static io.trueautomation.client.TrueAutomationHelper.ta;
         
         public class exampleTest {
             private TrueAutomationDriver driver;
             private By loginBtn = By.cssSelector(ta("ta:mainPage:loginBtn", "a.login-btn"));
             private By signupBtn = By.cssSelector(ta("ta:mainPage:signupBtn", "div.sign-up-container > a"));
             private By emailFl = By.name(ta("ta:loginPage:email", "email"));
         
             @BeforeTest
             public void beforeTest() {
                 DesiredCapabilities cap = DesiredCapabilities.chrome();
                 cap.setBrowserName("chrome");
                 cap.setPlatform(Platform.ANY);
                 cap.setCapability("taRemoteUrl", "http://localhost:4444/wd/hub");
                 driver = new TrueAutomationDriver(cap);
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

6. To run your test file use the command below in your terminal
    ```bash
    mvn -Dtest=exampleTest test
    ```
7. A new chrome window will be opened test actions should be performed. You’ll get the info in terminal:

    ![Test output](_images/java-grid-test.png 'Test output')

The test ran and was successful.

Check out an example of an actual test here: https://github.com/pyavchik/trueautomationGRID.git