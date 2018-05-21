# Creating your first test in TrueAutomation using Java/Maven

1. Initialize TrueAutomation project on your machine in the preferred folder. (for details checkout the [initializing guide](initializing.md))

2. Open your project in your integrated development environment (IDE)

3. Create simple test file

   It can look like this if it is the very first time you run TrueAutomation

      ```java
         import io.trueautomation.client.driver.TrueAutomationDriver;
         import org.openqa.selenium.By;
         import org.openqa.selenium.WebDriver;
         import org.testng.annotations.AfterTest;
         import org.testng.annotations.BeforeTest;
         import org.testng.annotations.Test;

         import java.util.concurrent.TimeUnit;

         import static io.trueautomation.client.TrueAutomationHelper.ta;

         public class exampleTest {
             private WebDriver driver;
             private By loginBtn = By.cssSelector(ta("loginBtn", "a.login-btn"));
             private By signupBtn = By.cssSelector(ta("signupBtn", "div.sign-up-container > a"));
             private By emailFl = By.name(ta("emailFl", "email"));

             @BeforeTest
             public void beforeTest() {
                 driver = new TrueAutomationDriver();
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

   It can look like this, if you have previously run TrueAutomation

   ```java
          import io.trueautomation.client.driver.TrueAutomationDriver;
          import org.openqa.selenium.By;
          import org.openqa.selenium.WebDriver;
          import org.testng.annotations.AfterTest;
          import org.testng.annotations.BeforeTest;
          import org.testng.annotations.Test;

          import java.util.concurrent.TimeUnit;

          import static io.trueautomation.client.TrueAutomationHelper.ta;

          public class exampleTest {
              private WebDriver driver;

              @BeforeTest
              public void beforeTest() {
                  driver = new TrueAutomationDriver();
                  driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);
              }

              @Test
              public void exampleTest() {
                  driver.get("https://trueautomation.io");

                  driver.findElement(By.cssSelector(ta("loginBtn"))).click();
                  driver.findElement(By.cssSelector(ta("signupBtn"))).click();

                  driver.findElement(By.name(ta("emailFl"))).sendKeys("your@mail.com");
              }

              @AfterTest
              public void afterTest() {
                  driver.quit();
              }
          }
         ```
4. To run your test file use the command below in your terminal:

   ```bash
    mvn -Dtest=exampleTest test
   ```

5. A new chrome window will be opened test actions should be performed. You’ll get the info in terminal:

    ![Test output](_images/java-test.png 'Test output')

The test ran and was successful.

Check out an example of an actual test here:  https://github.com/shapovalovei/trueautomation-testng