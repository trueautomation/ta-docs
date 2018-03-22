?> still in a development phase.

### API example: 

```ruby
# Find by: id, xpath, css, name , tag name, class, class_name
 
element = driver.find_element(:id, ta('id:input', 'field-id'))
element.send_keys("Hello TA! I found this element by 'id'")

element = driver.find_element(:name, ta('css:input', 'input#field-id'))
element.send_keys("Hello TA! I found this element by 'css'")

element = driver.find_element(:xpath, ta('xpath:input', "//*[@class='class-param']"))
element.send_keys("Hello TA! I found this element by 'xpath'")

element = driver.find_element(:css, ta('name:input', 'field-name'))
element.send_keys("Hello TA! I found this element by 'name'")


element = driver.find_element(:tag_name, ta('tag_name:input', 'input'))
element.send_keys("Hello TA! I found this element by 'tag_name'")

element = driver.find_element(:class, ta('class:input', 'class-param'))
element.send_keys("Hello TA! I found this element by 'class'")

element = driver.find_element(:class_name, ta('class_name:input', 'class-param'))
element.send_keys("Hello TA! I found this element by 'class_name'")


# Links by: link, link_text, partial_link_text
 
driver.find_element(:link, ta('link:link', 'TA best framework'))
driver.find_element(:link_text, ta('link:link_text', 'TA best framework'))
driver.find_element(:partial_link_text, ta('link:partial', 'TA best framework'))

#Or you can use only true automation locators. See example below

driver.find_element(:link, ta('link:link'))
driver.find_element(:link_text, ta('link:link_text'))
driver.find_element(:partial_link_text, ta('link:partial'))
```