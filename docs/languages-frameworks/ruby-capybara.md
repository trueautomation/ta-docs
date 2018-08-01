# Capybara

Before using the following tools, please make sure that you have:
- [Registered TrueAutomation.IO account](https://app.trueautomation.io/auth/signup)
- [Installed TrueAutomation client](install-client.md ':target=_blank')
- [Initialized project](initializing.md ':target=_blank')

## RemoteWebDriver
TrueAutomation supports [RemoteWebDriver](https://github.com/SeleniumHQ/selenium/wiki/RemoteWebDriver). To use it, set the following parameters into TrueAutomationDriver:
- `browser: :remote`;
- remote address of web driver or hub.

```ruby
Capybara.register_driver :remote do |app|
  TrueAutomation::Driver::Capybara.new(app, browser: :remote, url: 'http://remote_adress')
end
```

Here is the example of the `spec_helper.rb`, using RemoteWebDriver:

```ruby
require 'bundler/setup'
require 'ostruct'
require 'selenium-webdriver'
require 'rspec'
require 'rspec-steps'
require 'capybara/rspec'
require 'true_automation/rspec'
require 'true_automation/driver/capybara'

def camelize(str)
  str.split('_').map {|w| w.capitalize}.join
end

spec_dir = File.dirname(__FILE__)
$LOAD_PATH.unshift(spec_dir)

$data = {}
Dir[File.join(spec_dir, 'fixtures/**/*.yml')].each {|f|
  title = File.basename(f, '.yml')
  $data[title] = OpenStruct.new(YAML::load(File.open(f)))
}

$data = OpenStruct.new($data)
Dir[File.join(spec_dir, 'support/**/*.rb')].each {|f| require f}

RSpec.configure do |config|
  Capybara.register_driver :true_automation_driver do |app|
    TrueAutomation::Driver::Capybara.new(app, browser: :remote, url: 'http://remote_adress')
  end

  Capybara.configure do |capybara|
    capybara.run_server = false
    capybara.default_max_wait_time = 5

    capybara.default_driver = :true_automation_driver
  end

  config.include Capybara::DSL
  config.include TrueAutomation::DSL

  Dir[File.join(spec_dir, 'support/**/*.rb')].each {|f|
    base = File.basename(f, '.rb')
    klass = camelize(base)
    config.include Module.const_get(klass)
  }
end
```

Check out an example of an actual test here: https://github.com/pyavchik/remoteWebdriver

## GRID 
TrueAutomation supports [Selenium GRID](https://github.com/SeleniumHQ/selenium/wiki/Grid2).

Firstly you need to download the Selenium Standalonde Server from [here](https://docs.seleniumhq.org/download/) to folder with your project

![Selenium standalone server](../_images/seleniumStandaloneServer.png 'Test output')
    
On your computer go to Terminal and launch grid hub
```bash
java -jar selenium-server-standalone-3.13.0.jar -role hub
```

![Hub start](../_images/hub_start.png 'Test output')

On your computer go to Terminal and launch grid node
```bash
java -jar selenium-server-standalone-3.13.0.jar -role node -hub http://localhost:4444/grid/register -port 5556
```
![Node start](../_images/node_start.png 'Test output')

Here is the example of the test, using GRID:

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

To run your test file use the command below in your terminal
```bash
mvn -Dtest=exampleTest test
```
A new chrome window will be opened test actions should be performed. You’ll get the info in terminal:

   ![Test output](../_images/java-grid-test.png 'Test output')

The test ran and was successful.

Check out an example of an actual test here: https://github.com/pyavchik/trueautomationGRID.git


## API example

```ruby
   # Find by: id, xpath, css, name
   find(:id, ta('pageName:moduleName:objectName', 'id-1'))
   find(:css, ta('pageName:moduleName:objectName', "a#input"))
   find(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))

   # iframe
   within_frame(:xpath, ta('pageName:moduleName:objectName',"//iframe[@class='iframe']")) do
       ...
   end

   # Clicking links and buttons by id and text
   click_link(ta('pageName:moduleName:objectName', 'id-1'))
   click_link(ta('pageName:moduleName:objectName', 'Forgot password?'))

   # Radio buttons by id and text
   choose(ta('pageName:moduleName:objectName', 'radio1'))
   choose(ta('pageName:moduleName:objectName', 'Option 1'))

   # Checkboxes by id and text
   check(ta('pageName:moduleName:objectName', 'id-1'))
   check(ta('pageName:moduleName:objectName', 'Choice A'))
   uncheck(ta('pageName:moduleName:objectName', 'id-1'))
   uncheck(ta('pageName:moduleName:objectName', 'Choice A'))

   # Fill in
   fill_in(ta('pageName:moduleName:objectName', 'id-1'), with: 'someText')
   fill_in(ta('pageName:moduleName:objectName', 'Email Address'), with: 'someText')

   # Find all (page.all() / find_all())
   find_all(:id, ta('pageName:moduleName:objectName', 'id-1'))
   find_all(:css, ta('pageName:moduleName:objectName', "a#input"))
   find_all(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))

   # Find button
   find_button(ta('pageName:moduleName:objectName', 'id-1'))
   find_button(ta('pageName:moduleName:objectName', 'someText'))

   # Find link
   find_link(ta('pageName:moduleName:objectName', 'id-1'))
   find_link(ta('pageName:moduleName:objectName', 'someText'))

   # Find field
   find_field(ta('pageName:moduleName:objectName', 'id-1'))
   find_field(ta('pageName:moduleName:objectName', 'someText'))

   # First
   first(:id, ta('pageName:moduleName:objectName', 'id-1'))
   first(:css, ta('pageName:moduleName:objectName', "a#input"))
   first(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))

   # Click button & link
   click_button(ta('pageName:moduleName:objectName','someText'))
   click_link_or_button(ta('pageName:moduleName:objectName', 'id-1'))

   # Select
   select 'someText', from: ta('pageName:moduleName:objectName', 'someText')
   select 'someText', from: ta('pageName:moduleName:objectName', 'id-1')
```


```ruby
    # assert_all_of_selectors
    assert_all_of_selectors(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))
    assert_all_of_selectors(:css, ta('pageName:moduleName:objectName', 'a#input'))
    assert_all_of_selectors(:id, ta('pageName:moduleName:objectName', 'id-1'))

    # assert_selector
    assert_selector(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))
    assert_selector(:css, ta('pageName:moduleName:objectName', 'a#input'))
    assert_selector(:id, ta('pageName:moduleName:objectName', 'id-1'))

    # has_button?
    has_button?(ta('pageName:moduleName:objectName', 'someText'))
    has_button?(ta('pageName:moduleName:objectName', 'id-1'))

    # has_checked_field?
    has_checked_field?(ta('pageName:moduleName:objectName', 'someText'))
    has_checked_field?(ta('pageName:moduleName:objectName', 'id-1'))

    # has_css?
    has_css?(ta('pageName:moduleName:objectName', 'a#input'))

    # has_field?
    has_field?(ta('pageName:moduleName:objectName', 'someText'))
    has_field?(ta('pageName:moduleName:objectName', 'id-1'))

    # has_link?
    has_link?(ta('pageName:moduleName:objectName', 'id-1'))
    has_link?(ta('pageName:moduleName:objectName', 'someText'))

    # has_selector?
    has_selector?(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))
    has_selector?(:css, ta('pageName:moduleName:objectName', 'a#input'))
    has_selector?(:id, ta('pageName:moduleName:objectName', 'id-1'))

    # has_table?
    has_table?(ta('pageName:moduleName:objectName', 'someText'))
    has_table?(ta('pageName:moduleName:objectName', 'id-1'))

    # has_xpath?
    has_xpath?(ta('pageName:moduleName:objectName', "//div[@class='btn']"))
```