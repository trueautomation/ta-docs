# Capybara
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

## RemoteWebDriver
TrueAutomation supports [RemoteWebDriver](https://github.com/SeleniumHQ/selenium/wiki/RemoteWebDriver). To use it, set the following parameters into TrueAutomationDriver:
- `browser: :remote`;
- remote address of web driver or hub.

```ruby
Capybara.register_driver :remote do |app|
  TrueAutomation::Driver::Capybara.new(app, browser: :remote, url: 'http://<driver_host>:<driver_port>')
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
    TrueAutomation::Driver::Capybara.new(app, browser: :remote, url: 'http://<driver_host>:<driver_port>')
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