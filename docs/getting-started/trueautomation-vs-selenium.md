# TrueAutomation vs Selenium

One of the main tasks of TA is to solve problem of working with unstable locators. The Object Repository and SmartLocators are exactly used for this. But as a matter of fact - they are not actually locators.
A regular locator that is currently used in many tools is actually a path to the element that is dependent on technology, page hierarchy, etc. That is why, whenever anything is changed, the locator is not valid anymore. That’s the reason why we have moved away from the idea of using old-school locators. The whole idea of them is broken and requires tons of maintenance.

What we call a SmartLocator is a unique footprint of an element. This is how we build it:
During the first API call we collect information on elements, element attributes, dependencies between elements, page information. Once information is collected we build a unique footprint of the element based on it. That allows us not to depend on actual locators and thus minimize further maintenance and guarantee, that the element will be found even if it is dramatically changed. In other words, TrueAutomation SmartLocator is just and an alias for the set of unique parameters that characterize a particular element and helps us find it.

The Object Repository is a collection of object and properties. Initially, it is designed for caching of test objects. Afterwards, one you have already objects in the repository, it will help to detect elements on the web page more precisely even in case when their parameters were partially changed. Objects are added to your project repository when you run tests with them in TrueAutomation for the 1st time. Thus, TA will solve this problem when Selenium doesn’t perform such functions at all.

There is a special helper `ta(name, locator)`.

In order to use TrueAutomation Smart Locators use `ta(ta_name, locator)` instead of your locators.

`ta_name` - is TrueAutomation Element name. We recommend to use namespaced syntax. E.g. `pageName:widgetName:elementName`

`locator` - is any Selenium locator to use to find element for the first time. If you change initial locator in your code, TrueAutomation element record will be rewritten during next test run

Object repository located: `https://app.trueautomation.io/app/projects/<project-name>/elements`

## Capybara example {docsify-ignore}

Capybara without TrueAutomation locator
```ruby
find(:xpath, '//locator'))
```

Capybara with TrueAutomation locator
```ruby
find(:xpath, ta('pageName:moduleName:objectName', '//locator'))
```

Once your object are in a repository and you want to use it in a test. You can do it like this:

```ruby
find(ta('pageName:moduleName:objectName'))
```

## Java example {docsify-ignore}

Java without TrueAutomation locator
```java
driver.findElement(By.xpath("//locator"));
```

Java with TrueAutomation locator
```java
driver.findElement(By.xpath(ta('pageName:moduleName:objectName', '//locator')));
```

Once your object are in a repository and you want to use them in a test. You can do this using the "byTa" method
```java
driver.findElement(byTa('pageName:moduleName:objectName'));
```
