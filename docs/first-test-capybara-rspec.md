# Creating your first test in TrueAutomation using Capybara/RSpec

> [Example project on GitHub.](https://github.com/shapovalovei/trueautomation-capybara) 

1. Initialize TrueAutomation project on your machine in the preferred folder. (for details checkout the initializing project [automatically](project-init-automatically.md) or [manually](project-init-manually.md#initializing-javatestng-project)

2. Open your project in your integrated development environment (IDE)

3. Open folder `spec/` inside of your project, if you don’t have one - create it.

4. Create folder `test_scenario/` in `spec/` folder

5. Create simple test file in `test_scenario/` folder
    
It can look like this if it is the very first time you run TrueAutomation 
  
```ruby

require 'spec_helper'

describe 'True Automation Demo Test' do
  it 'Fill form and authorize' do
    # Navigate on test page
    visit 'http://www.trueautomation-demo.inf.ua'

    # Fill user identifier Id and password
    find(:xpath, ta('loginPage:userEmail', "//input[@placeholder='email']")).set('team@trueautomation.io')
    find(:xpath, ta('loginPage:userPassword', "//input[@type='password']")).set('password')

    # Select `Remember me` checkbox
    find(:id, ta('loginPage:rememberMe', 'checkboxG1')).click

    # Click authorize button
    find(:xpath, ta('loginPage:authorizeBtn', "//button[@class='btn-radius']")).click
  end
end

```

It can look like this, if you have previously run TrueAutomation

```ruby
require 'spec_helper'

describe 'True Automation Demo Test' do
  it 'Fill form and authorize' do
    # Navigate on test page
    visit 'http://www.trueautomation-demo.inf.ua'

    # Fill user identifier Id and password
    find(ta('loginPage:userEmail')).set('team@trueautomation.io')
    find(ta('loginPage:userPassword')).set('password')

    # Select `Remember me` checkbox
    find(ta('loginPage:rememberMe')).click

    # Click authorize button
    find(ta('loginPage:authorizeBtn')).click
  end
end
```

6. To run your test file use the command below in your terminal:

```sh
rspec spec/test_scenario/*rb
```

7. A new chrome window will be opened test actions should be performed. You’ll get the info in terminal:

![Test output](_images/pass-test-output-capybara-rspec.png 'Test output')

The test ran and was successful.


## API example: 
```ruby
# Find by: id, xpath, css, name 
find(:id, ta('pageName:moduleName:objectName', 'id-1'))
find(:css, ta('pageName:moduleName:objectName', "a#input"))
find(:name, ta('pageName:moduleName:objectName', 'fieldName'))
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
find_all(ta('pageName:moduleName:objectName', 'someText'))
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
first(ta('pageName:moduleName:objectName', 'someText'))
first(:id, ta('pageName:moduleName:objectName', 'id-1'))
first(:css, ta('pageName:moduleName:objectName', "a#input"))
first(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))

# Click button & link
click_button(ta('pageName:moduleName:objectName','someText'))
click_link_or_button(ta('pageName:moduleName:objectName', 'id-1'))


# Select
select ta('pageName:moduleName:objectName', 'someText'), from: ta('pageName:moduleName:objectName', 'someText')
select ta('pageName:moduleName:objectName', 'someText'), from: ta('pageName:moduleName:objectName', 'id-1')


# Assertions 
# assert_all_of_selectors
assert_all_of_selectors('label', text: ta('pageName:moduleName:objectName', 'someText'))
assert_all_of_selectors(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))
assert_all_of_selectors(:css, ta('pageName:moduleName:objectName', 'a#input'))
assert_all_of_selectors(:id, ta('pageName:moduleName:objectName', 'id-1'))

# assert_selector
assert_selector('label', text: ta('pageName:moduleName:objectName', 'someText'))
assert_selector(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))
assert_selector(:css, ta('pageName:moduleName:objectName', 'a#input'))
assert_selector(:id, ta('pageName:moduleName:objectName', 'id-1'))

# assert_text
assert_text(ta('pageName:moduleName:objectName', 'someText'))

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

# has_select?
has_select?(ta('pageName:moduleName:objectName', 'someText'), with_options: ta('pageName:moduleName:objectName', %w[someText1 someText]))
has_select?(ta('pageName:moduleName:objectName', 'id-1'), with_options: ta('pageName:moduleName:objectName', %w[someText1 someText]))

# has_selector?
has_selector?('label', text: ta('pageName:moduleName:objectName', 'someText'))
has_selector?(:xpath, ta('pageName:moduleName:objectName', "//div[@class='btn']"))
has_selector?(:css, ta('pageName:moduleName:objectName', 'a#input'))
has_selector?(:id, ta('pageName:moduleName:objectName', 'id-1'))

# has_table?
has_table?(ta('pageName:moduleName:objectName', 'someText'))
has_table?(ta('pageName:moduleName:objectName', 'id-1'))

# has_text?
has_text?(ta('pageName:moduleName:objectName', 'someText'))

# has_xpath?
has_xpath?(ta('pageName:moduleName:objectName', "//div[@class='btn']"))

xpath = XPath.generate { |x| x.descendant(:p) }
has_xpath?(ta('pageName:moduleName:objectName', xpath))
```