# Creating your first test in TrueAutomation using Capybara + RSpec  

### Test example:

```ruby
require 'spec_helper'

describe 'True Automation Demo Test' do
  it 'Fill form and authorize' do
    # Navigate on test page
    visit 'http://www.trueautomation-demo.inf.ua'

    # Fill user identifier Id and password
    find(:xpath, ta('demo:userId', "//input[@placeholder='email']")).set('team@trueautomation.io')
    find(:xpath, ta('demo:userPassword', "//input[@type='password']")).set('password')

    # Select `Remember me` checkbox
    find(:id, ta('demo:rememberMe', 'checkboxG1')).click

    # Click authorize button
    find(:xpath, ta('demo:authorizeBtn', "//button[@class='btn-radius']")).click
  end
end
```

### Test example uses only ta locators:
```Ruby
require 'spec_helper'

describe 'True Automation Demo Test' do
  it 'Fill form and authorize' do
    # Navigate on test page
    visit 'http://www.trueautomation-demo.inf.ua'

    # Fill user identifier Id and password
    find(ta('demo:userId')).set('team@trueautomation.io')
    find(ta('demo:userPassword')).set('password')

    # Select `Remember me` checkbox
    find(ta('demo:rememberMe')).click

    # Click authorize button
    find(ta('demo:authorizeBtn')).click
  end
end
```

#### API example: 
```Ruby
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