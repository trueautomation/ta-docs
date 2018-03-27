# Using smart locators (Object repository)

Object Repository is a collection of object and properties. Initially it is designed for caching of test objects. Afterwards (one you already have objects in the repository) it will help to more precisely detect elements on the web page even in case when their parameters were partially changed. Objects are added to your project repository when you run tests with them in TrueAutomation for the 1st time.  

There is a special helper ta(name, locator) defined in trueautomation gem.

In order to use TrueAutomation Smart Locators use ta(ta_name, locator) instead of your locators.

Example: 

```ruby
find(:xpath, ta('pageName:moduleName:objectName', '//initialLocator'))
```

Once your object are in a repository and you want to use them in a text. You can do it like this:

```ruby
find(ta('pageName:moduleName:objectName'))
```

We suggest you to use namespaced names for your object. e.g.: `pageName:moduleName:objectName`

But you can use a string of any kind. Initial locator is used to locate object for the first time. If you change initial locator value object will be rewritten. 