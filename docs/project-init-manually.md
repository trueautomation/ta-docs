# Initializing project (Manual)

## Initializing Capybara/RSpec project

> This clause explains how to implement TrueAutomation into Capybara/RSpec step by step:
 
1. Add the following line to your `Gemfile`
```ruby
gem 'true_automation'
```

2. Run command
```bash
bundle install
```

3. Load RSpec support by adding the following line into your `spec_helper.rb` file:
```ruby
require 'true_automation/rspec'
```

4. Load Capybara support by adding the following line into your `spec_helper.rb` file:
```ruby
require 'true_automation/driver/capybara'
```

5. Register the new WebDriver for Capybara in your `spec_helper.rb` file:
```ruby
Capybara.register_driver :true_automation_driver do |app|
 TrueAutomation::Driver::Capybara.new(app)
end
```

6. Update default driver in your `spec_helper.rb` file:
```ruby
Capybara.configure do |capybara|
  capybara.default_driver = :true_automation_driver
end
```
 
7. Make TrueAutomation DSL available
```ruby
config.include TrueAutomation::DSL
```

8. Create `trueautomation.json` with following line. And setup `"projectName"` from [cloud](https://app.trueautomation.io/app/main)
```json
{
  "projectName": "ta-project-name"
}
```

9. Then go to the ["Creating your first test in TrueAutomation using Capybara/RSpec"](first-test-capybara-rspec.md#creating-your-first-test-in-trueautomation-using-capybararspec) and create your first test.


## Initializing Java/TestNG project

> This clause explains how to implement True Automation into Java/TestNG step by step:

1. Add the repositories information inside the `<project>` tag in the `pom.xml` file:
```xml
<repositories>
    <repository>
        <id>trueautomation-io</id>
        <name>TrueAutomation.IO MVN Repository</name>
        <url>https://mvn.trueautomation.io/artifactory/trueautomation</url>
    </repository>
</repositories>       
```

2. Add the dependency information inside the `<dependencies>` tag in the `pom.xml` file:
```xml
<dependency>
    <groupId>io.trueautomation</groupId>
    <artifactId>trueautomation-client</artifactId>
    <version>0.3.0</version>
</dependency>  
```

3. Create TrueAutomation Driver by adding the following lines into `java` file:
```java
import io.trueautomation.client.driver.TrueAutomationDriver;
WebDriver driver = new TrueAutomationDriver();
```

4. Add the following linet into java file and use TA locators:
```java
import static io.trueautomation.client.TrueAutomationHelper.ta;
```

5. Create `trueautomation.json` with following line. And setup `"projectName"` from [cloud](https://app.trueautomation.io/app/main)
```json
{
  "projectName": "ta-project-name"
}
```
6. Then go to the ["Creating your first test in TrueAutomation using Java/TestNG"](first-test-java-testng.md#creating-your-first-test-in-trueautomation-using-javatestng) and create your first test.

