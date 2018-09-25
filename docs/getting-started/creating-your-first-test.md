# Creating your first test

## TrueAutomation using Java/Maven

1. Initialize TrueAutomation project on your machine in the preferred folder. (for details checkout the [initializing guide](/initializing/initializing-automatically.md))

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

         import static io.trueautomation.client.TrueAutomationHelper.*;

         public class exampleTest {
             private WebDriver driver;
             private By loginBtn = By.cssSelector(ta("ta:mainPage:loginBtn", "a.login-btn"));
             private By signupBtn = By.cssSelector(ta("ta:mainPage:signupBtn", "div.sign-up-container > a"));
             private By emailFl = By.name(ta("ta:loginPage:email", "email"));

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

   It can look like this if you have previously run TrueAutomation

   ```java
          import io.trueautomation.client.driver.TrueAutomationDriver;
          import org.openqa.selenium.By;
          import org.openqa.selenium.WebDriver;
          import org.testng.annotations.AfterTest;
          import org.testng.annotations.BeforeTest;
          import org.testng.annotations.Test;

          import java.util.concurrent.TimeUnit;

          import static io.trueautomation.client.TrueAutomationHelper.*;

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

                  driver.findElement(byTa("ta:mainPage:loginBtn")).click();
                  driver.findElement(byTa("ta:mainPage:signupBtn")).click();

                  driver.findElement(byTa("ta:loginPage:email")).click();
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

    ![Test output](../_images/java-test.png 'Test output')

The test ran and was successful.

**Check out an example of an actual test here:  https://github.com/shapovalovei/trueautomation-java**

## TrueAutomation test using Capybara/RSpec

1. Initialize TrueAutomation project on your machine in the preferred folder. (for details checkout the [initializing guide](/initializing/initializing-automatically.md))

2. Open your project in your integrated development environment (IDE).

3. Open folder `spec/` inside of your project, if you don’t have one - create it.

4. Create simple test file in `spec/` folder.

   It can look like this if it is the very first time you run TrueAutomation

   ```ruby
    require 'spec_helper'

    describe 'TrueAutomation.IO capybara example' do
      it 'Test example' do
        visit 'https://trueautomation.io/'

        find(:css, ta('ta:mainPage:loginBtn', 'a.login-btn')).click

        find(:css, ta('ta:mainPage:signupBtn', 'div.sign-up-container > a')).click

        fill_in ta('ta:loginPage:email', 'email'), with: 'your@mail.com'
        sleep 3
      end
    end
   ```

   It can look like this, if you have previously run TrueAutomation

   ```ruby
    require 'spec_helper'

    describe 'TrueAutomation.IO capybara example' do
      it 'Test example' do
        visit 'https://trueautomation.io/'

        find(ta('ta:mainPage:loginBtn')).click

        find(ta('ta:mainPage:signupBtn')).click

        fill_in ta('ta:loginPage:email'), with: 'your@mail.com'
        sleep 3
      end
    end
   ```

5. To run your test file use the command below in your terminal:

   ```bash
    rspec spec/test_scenario/*rb
   ```

6. A new chrome window will be opened test actions should be performed. You’ll get the info in terminal:

    ![Test output](../_images/capybara-test.png 'Test output')

The test ran and was successful.

**Check out an example of an actual test here:  https://github.com/shapovalovei/trueautomation-capybara**