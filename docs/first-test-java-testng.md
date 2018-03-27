# Creating your first test in TrueAutomation using Java/TestNG

1. Initialize TrueAutomation project on your machine in the preferred folder. (for details checkout the initializing project [automatically](project-init-automatically.md) or [manually](project-init-manually.md#initializing-javatestng-project) or [example project from GitHub](https://github.com/shapovalovei/trueautomation-testng)) 

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
          
          import static io.trueautomation.client.TrueAutomationHelper.ta;
          
          public class testScenario {
              private WebDriver driver;
              private By email = By.xpath(ta("loginPage:userEmail", "//input[@placeholder='email']"));
              private By password = By.xpath(ta("loginPage:userPassword", "//input[@type='password']"));
              private By authBtn = By.xpath(ta("loginPage:authorizeBtn", "//button[@class='btn-radius']"));
              private By rememberMe = By.id(ta("loginPage:rememberMe", "checkboxG1"));
          
              @BeforeTest
              public void beforeTest() {
                  driver = new TrueAutomationDriver();
              }
          
              @Test
              public void test() {
                  /* Navigate on test page */
                  driver.get("http://www.trueautomation-demo.inf.ua");
          
                  /* Fill user identifier Id and password */
                  driver.findElement(email).sendKeys("team@trueautomation.io");
                  driver.findElement(password).sendKeys("password");
          
                  /* Select `Remember me` checkbox */
                  driver.findElement(rememberMe).click();
          
                  /* Click authorize button */
                  driver.findElement(authBtn).click();
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
          
          import static io.trueautomation.client.TrueAutomationHelper.ta;
          
          public class testScenario {
              private WebDriver driver;
              private By email = By.xpath(ta("loginPage:userEmail", "//input[@placeholder='email']"));
              private By password = By.xpath(ta("loginPage:userPassword", "//input[@type='password']"));
              private By authBtn = By.xpath(ta("loginPage:authorizeBtn", "//button[@class='btn-radius']"));
              private By rememberMe = By.id(ta("loginPage:rememberMe", "checkboxG1"));
          
              @BeforeTest
              public void beforeTest() {
                  driver = new TrueAutomationDriver();
              }
          
              @Test
              public void test() {
                  /* Navigate on test page */
                  driver.get("http://www.trueautomation-demo.inf.ua");
          
                  /* Fill user identifier Id and password */
                  driver.findElement(email).sendKeys("team@trueautomation.io");
                  driver.findElement(password).sendKeys("password");
          
                  /* Select `Remember me` checkbox */
                  driver.findElement(rememberMe).click();
          
                  /* Click authorize button */
                  driver.findElement(authBtn).click();
              }
          
              @AfterTest
              public void afterTest() {
                  driver.quit();
              }
          }
         ```
4. To run your test file use the command below in your terminal:

   ```sh
    mvn -Dtest=testScenario test
   ```

5. A new chrome window will be opened test actions should be performed. You’ll get the info in terminal:

    ![Test output](_images/pass-test-output-java-testng.png 'Test output')

The test ran and was successful.