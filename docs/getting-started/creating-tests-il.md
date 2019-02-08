## TrueAutomation with Java

1. Initialize TrueAutomation project on your machine in the preferred directory. For details checkout the [initializing guide](/initializing/initializing-automatically.md)

2. Open the project in your integrated development environment (IDE).

3. Create a new java class for your test by following the directory: `./src/test/java/*.java` inside your project.

4. First you need to import the `TrueAutomationDriver` class and the `ta` method, which belongs to the `TrueAutomationHelper` class:

```java
import io.trueautomation.client.driver.TrueAutomationDriver;
import static io.trueautomation.client.TrueAutomationHelper.ta;
```

5. Then write your test, by wrapping an element locators in special helper: `ta(ta_name, locator)`. More info: [here](/getting-started/ta-locators.md)

```java
private By loginBtn = By.cssSelector("a.login-btn"); // before
private By loginBtn = By.cssSelector(ta("ta:mainPage:loginBtn", "a.login-btn")); // after
```

The final test will look like this:

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

You can also find this example in the project!

Once your elements are recorded, you can get rid of Regular locators in your code and use only TA locators. To do this, use the special method `byTa`:

```java
import static io.trueautomation.client.TrueAutomationHelper.byTa;
```

As a result, the test will look like this:

```java
import io.trueautomation.client.driver.TrueAutomationDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import java.util.concurrent.TimeUnit;

import static io.trueautomation.client.TrueAutomationHelper.byTa;

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

4. To run your test file use the command below in your command line:

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

5. A new browser window will be opened, test actions will be performed. You’ll get the test info in your command line:

<!-- tabs:start -->
#### **Maven**
![Test output](../_images/maven-test.png 'Test output')

#### **Gradle**
![Test output](../_images/gradle-test.png 'Test output')
<!-- tabs:end -->

**Check out an example of an actual test here:  https://github.com/shapovalovei/trueautomation-java**

## TrueAutomation with Capybara/RSpec

1. Initialize TrueAutomation project on your machine in the preferred directory. (for details checkout the [initializing guide](/initializing/initializing-automatically.md)).

2. Open the project in your integrated development environment (IDE).

3. Create a file for your test by following the directory: `./spec/test_scenario/*.rb` inside your project.

4. First you need to add the `spec_helper` module:

```ruby
require 'spec_helper'
```

5. Then write your test, by wrapping an element locators in special helper: `ta(ta_name, locator)`. More info: [here](/getting-started/ta-locators.md)

```ruby
find(:css, 'a.login-btn').click # before
find(:css, ta('ta:mainPage:loginBtn', 'a.login-btn')).click # after
```

The final test will look like this:

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

You can also find this example in the project!
  
Once your elements are recorded, you can get rid of Regular locators in your code and use only TA locators:

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

6. To run your test file use the command below in your command line:

```bash
rspec spec/test_scenario/*.rb
```

7. A new browser window will be opened, test actions will be performed. You’ll get the test info in your command line:

![Test output](../_images/capybara-test.png 'Test output')

**Check out an example of an actual test here:  https://github.com/shapovalovei/trueautomation-capybara**

## TrueAutomation with JavaScript/WebdriverIO

1. Initialize TrueAutomation project on your machine in the preferred directory, (checkout the [initializing guide](/initializing/initializing-automatically.md) for details).

2. Open the project in your integrated development environment (IDE).

3. Create a file for your test by following the directory: `./test/specs/**/*.js` inside your project.

4. First you need to load the `trueautomation-helper` module:

```javascript
const ta = require('trueautomation-helper').ta;
```
5. Then write your test, by wrapping an element locators in special helper: `ta(ta_name, locator)`. More info: [here](/getting-started/ta-locators.md)

```javascript 
$('a.login-btn').click(); // before 
$(ta('loginBtn', 'a.login-btn')).click(); // after
```

The final test will look like this:

```javascript
const ta = require('trueautomation-helper').ta;

describe('TrueAutomation.IO + WebdirverIO', () => {   
   it('Test example', () => {
        browser.setTimeout({ 'implicit': 5000 });
        
        browser.url('https://trueautomation.io');   
        $(ta('loginBtn', 'a.login-btn')).click();
        $(ta('signUpBtn', 'div.sign-up-container > a')).click();
        $(ta('emailFld', "[name='email']")).setValue('your@gmail.com');
   });
});
```

You can also find this example in the project!

Once your elements are recorded, you can get rid of Regular locators in your code and use only TA locators:

```javascript
const ta = require('trueautomation-helper').ta;
  
describe('TrueAutomation.IO + WebdirverIO', () => {   
   it('Test example', () => {
       browser.setTimeout({ 'implicit': 5000 });
  
       browser.url('https://trueautomation.io');   
       $(ta('loginBtn')).click();
       $(ta('signUpBtn')).click();
       $(ta('emailFld')).setValue('your@gmail.com');  
   });  
});
```

6. Run `npm install` and then `npm test` to check your test. A new browser window will be opened, test actions will be performed. You’ll get the test info in your command line:

![Test output](../_images/wdio-test.png 'Test output')

**Check out an example of an actual test here:  https://github.com/shapovalovei/trueautomation-wdioV5**
