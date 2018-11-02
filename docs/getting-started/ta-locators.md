There is a special helper `ta(name, locator)`.

In order to use TrueAutomation Smart Locators use `ta(ta_name, locator)` instead of your locators.

`ta_name` - is TrueAutomation Element name. We recommend to use namespaced syntax. E.g. `pageName:widgetName:elementName`

`locator` - is any Selenium locator (ID, name, XPath, etc).

Object repository located: `https://app.trueautomation.io/app/projects/<project-name>/elements`

## How it works: {docsify-ignore}

Selenium locators (`Initial locators`) are used to find element for the first time, in this way pointing to the element that should be written to the object repository using `TA locator`. Both the TA locator and the Initial locator are saved in the object repository. 

The next time running the test, we compare the Initial locator of element in the object repository and the Initial locator in your code. If the Initial locator in code has not changed, then a TA "smart locator" will be used to find the element. Otherwise, if the Initial locator was changed, then a new Initial locator will be used to locate the element and the TA locator will be overwritten in the object repository.

This way, you use TA "smart locators" in your tests, and Initial locators are used only to specify the element that you should write or rewrite. At the same time, if elements are already recorded to the object repository, you can get rid of Initial locators in your code and use only TA locators. [See examples when (only) TA locators are used below](https://trueautomation.io/docs/#/getting-started/ta-locators?id=capybara-example)

Also, do not forget that you can completely get rid of using the Initial locators when creating your tests via the [TrueAutomation.IO Element Picker](https://trueautomation.io/docs/#/getting-started/using-element-picker), which allows you to record the desired element on a web page by clicking on it with the mouse cursor.

## Capybara example {docsify-ignore}

Capybara without TrueAutomation locator:
```ruby
find(:xpath, '//locator'))
```

Capybara with TrueAutomation locator:
```ruby
find(:xpath, ta('pageName:moduleName:objectName', '//locator'))
```

Once your elements are in object repository and you want to use them in a test. You can do it like this:

```ruby
find(ta('pageName:moduleName:objectName'))
```

## Java example {docsify-ignore}

Java without TrueAutomation locator:
```java
driver.findElement(By.xpath("//locator"));
```

Java with TrueAutomation locator:
```java
import static io.trueautomation.client.TrueAutomationHelper.ta;

driver.findElement(By.xpath(ta('pageName:moduleName:objectName', '//locator')));
```

Once your elements are in object repository and you want to use them in a test. You can do this using the special `byTa` method:
```java
import static io.trueautomation.client.TrueAutomationHelper.byTa;

driver.findElement(byTa('pageName:moduleName:objectName'));
```
