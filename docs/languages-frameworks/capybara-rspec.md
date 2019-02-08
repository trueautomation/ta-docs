# Capybara

Before using the following tools, please make sure that you have:
- [Registered TrueAutomation.io account](https://app.trueautomation.io/auth/signup)
- [Installed TrueAutomation client](/getting-started/installation.md ':target=_blank')
- [Initialized project](/initializing/initializing-automatically.md ':target=_blank')

## RemoteWebDriver

TrueAutomation supports using [RemoteWebDriver](https://github.com/SeleniumHQ/selenium/wiki/RemoteWebDriver) in the Capybara/RSpec technology stack. To use RemoteWebDriver with TrueAutomation, set the following parameters into TrueAutomationDriver:
- the `browser: :remote` option;
- remote address of a browser driver or WebDriver Server;

```ruby
Capybara.register_driver :remote do |app|
  TrueAutomation::Driver::Capybara.new(app, browser: :remote, url: 'http://remote_adress')
end
```

Here is the example of the `spec_helper.rb` file for using RemoteWebDriver with TrueAutomation in this technology stack:

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

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-capybara-remoteWebDriver**

## GRID 

TrueAutomation supports using [Selenium GRID](https://www.seleniumhq.org/docs/07_selenium_grid.jsp) in the Capybara/RSpec technology stack.

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

Here is the example of using GRID with TrueAutomation in this technology stack:

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
  config.include Capybara::DSL
  config.include TrueAutomation::DSL
end

Capybara.configure do |capybara|
  capybara.run_server = false
  capybara.default_max_wait_time = 5

  Capybara.default_driver = :remote_browser
  capabilities = Selenium::WebDriver::Remote::Capabilities.chrome

  Capybara.register_driver :remote_browser do |app|
    grid_url = 'http://localhost:4444/wd/hub'
    Capybara::Selenium::Driver.new(:remote, url: grid_url, desired_capabilities: capabilities)
  end

  Dir[File.join(spec_dir, 'support/**/*.rb')].each {|f|
    base = File.basename(f, '.rb')
    klass = camelize(base)
    config.include Module.const_get(klass)
  }

end
```

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-capybara-grid**

## Appium

TrueAutomation supports [Appium](https://appium.io/)

To get started, make you have Appium and all of its dependencies installed. If you do not have Appium in place, please refer to its documentation to install it.

Run Appium server, using Terminal, appium desktop app. By default Appium is run on port number `4723`.

Example:

Set up driver for iOS (make sure that you use your device udid):

```ruby
Capybara.register_driver :true_automation_driver do |app|
      caps = Selenium::WebDriver::Remote::Capabilities.new
      caps['automationName'] = 'XCUITest'
      caps['platformName'] = 'iOS'
      caps['deviceName'] = 'iPhone X (11.4)'
      caps['udid'] = '1DA711FE-C66B-4538-9147-10852CF5F1ED'
      caps['browserName'] = 'safari'
      TrueAutomation::Driver::Capybara.new(app, browser: :remote,
                                           url: 'http://localhost:4723/wd/hub',
                                           desired_capabilities: caps)
    end
```

Set up driver for Android (make sure that you use your device udid):

```ruby
Capybara.register_driver :true_automation_driver do |app|
      caps = Selenium::WebDriver::Remote::Capabilities.new
      caps['platformName'] = 'Android'
      caps['browserName'] = 'chrome'
      caps['deviceName'] = 'Android'
      TrueAutomation::Driver::Capybara.new(app, browser: :remote,
                                           url: 'http://localhost:4723/wd/hub',
                                           desired_capabilities: caps)
    end

```

After all changes the spec_helper.rb should look like:

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
  config.include Capybara::DSL
  config.include TrueAutomation::DSL


  Capybara.register_driver :true_automation_driver do |app|
    caps = Selenium::WebDriver::Remote::Capabilities.new
    caps['automationName'] = 'XCUITest'
    caps['platformName'] = 'iOS'
    caps['deviceName'] = 'iPhone X (11.4)'
    caps['udid'] = '1DA711FE-C66B-4538-9147-10852CF5F1ED'
    caps['browserName'] = 'safari'
    TrueAutomation::Driver::Capybara.new(app, browser: :remote,
                                         url: 'http://localhost:4723/wd/hub',
                                         desired_capabilities: caps)

  end


  Capybara.configure do |capybara|
    capybara.run_server = false
    capybara.default_max_wait_time = 5
    capybara.default_driver = :true_automation_driver
  end


  Dir[File.join(spec_dir, 'support/**/*.rb')].each {|f|
    base = File.basename(f, '.rb')
    klass = camelize(base)
    config.include Module.const_get(klass)
  }

end

```

Before you run the test, make sure that you have updated capabilities(`deviceName`, `automationName`, `udid`, `platformName`, `browserName`) according to the capabilities of the device that is used for running the test.

**Check out an example of an actual test here: https://github.com/shapovalovei/trueautomation-capybara-remoteWebDriver**

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

<br>

## TrueAutomation capabilities

TrueAutomation supports all WebDriver capabilities and expands them with our internal capabilities.

#### TrueAutomation embedded drivers selection

There are internal capabilities for embedded drivers selection through the Desired Capabilities. These are special key and value pairs that are sent to the server in the JSON object when requesting a new automation session. They specify driver and its version that should be used in a test.

|**Key**| &nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp;**Type**&nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp; | **Description**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;     |
|:---:|:---:|:---|
|driver| string | The driver name being used. Should be one of: <br>- chromedriver<br>- geckodriver<br>- microsoftwebdriver<br>- safaridriver|
|driver_version| string | The driver version being used. If driver version is <br>not set, the test will be run with the latest driver <br>version.<br>|

**Example of using**

```ruby
Capybara.register_driver :true_automation_driver do |app|
TrueAutomation::Driver::Capybara.new(app, driver: 'chromedriver', driver_version: '2.42')
end
```

You can observe a list of current drivers and their versions using the `trueautomation driver list` command.
