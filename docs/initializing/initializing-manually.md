## Initializing Java/Maven project

This clause explains how to implement TrueAutomation into Java/Maven project step by step.
Firstly, you must have a fully configured and working Java/Maven project. If you do not have such a project, you can [clone our sample project with Github](https://github.com/shapovalovei/testng-example).

**And now take the following steps:**

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
    <version>0.3.7</version>
</dependency>  
```

3. Create TrueAutomation Driver by adding the following lines into `java` file:
```java
import io.trueautomation.client.driver.TrueAutomationDriver;
```
```java
WebDriver driver = new TrueAutomationDriver();
```

4. Add the following lines into java file and use TA locators:
```java
import static io.trueautomation.client.TrueAutomationHelper.*;
```

5. Create in project root `trueautomation.json` with following line. And setup `"projectName"` from [cloud](https://app.trueautomation.io/app/projects)
```json
{
  "projectName": "ta-project-name"
}
```
6. Then go to the [Creating your first test in TrueAutomation using Java/Maven](/getting-started/creating-your-first-test.md#creating-your-first-test-in-trueautomation-using-javamaven) and create your first test.

## Initializing Ruby/Capybara project

This clause explains how to implement TrueAutomation into Ruby/Capybara project step by step.
Firstly, you must have a fully configured and working Ruby/Capybara project. If you do not have such a project, you can [clone our sample project with Github](https://github.com/shapovalovei/capybara-example).

**And now take the following steps:**

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

8. Create in project root `trueautomation.json` with following line. And setup `"projectName"` from [cloud](https://app.trueautomation.io/app/projects)
```json
{
  "projectName": "ta-project-name"
}
```

9. Then go to the [Creating your first test in TrueAutomation using Capybara/RSpec](/getting-started/creating-your-first-test.md#trueautomation-test-using-capybararspec) and create your first test.
