# Selenium vs TrueAutomation ?

Object Repository is a collection of object and properties. Initially it is designed for caching of test objects. Afterwards (one you already have objects in the repository) it will help to more precisely detect elements on the web page even in case when their parameters were partially changed. Objects are added to your project repository when you run tests with them in TrueAutomation for the 1st time.  

There is a special helper `ta(name, locator)`.

In order to use TrueAutomation Smart Locators use `ta(ta_name, locator)` instead of your locators.

`ta_name` - is TrueAutomation Element name. We recommend to use namespaced syntax. E.g. `pageName:widgetName:elementName`

`locator` - is any Selenium locator to use to find element for the first time. If you change initial locator in your code, TrueAutomation element record will be rewritten during next test run

Object repository located: `https://app.trueautomation.io/app/projects/<project-name>/elements`

## Capybara example

Capybara without TrueAutomation locator
```ruby
find(:xpath, '//locator'))
```

Capybara with TrueAutomation locator
```ruby
find(:xpath, ta('pageName:moduleName:objectName', '//locator'))
```

Once your object are in a repository and you want to use them in a text. You can do it like this:

```ruby
find(ta('pageName:moduleName:objectName'))
```

## Java example

Java without TrueAutomation locator
```java
driver.findElement(By.xpath("//locator"))
```

Java with TrueAutomation locator
```ruby
driver.findElement(By.xpath(ta('pageName:moduleName:objectName', '//locator')))
```

Once your object are in a repository and you want to use them in a text. You can do it like this:

```ruby
driver.findElement(By.xpath(ta('pageName:moduleName:objectName')))
```
