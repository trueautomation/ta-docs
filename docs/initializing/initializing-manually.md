# Initializing manually

Follow the steps below to manually initialize a project and start writing tests (if you prefer to automatically initialize your project - please refer to [automatic initialization](/initializing/initializing-automatically.md) section).

## Initializing Java/Maven project

Use this section as a step-by-step instruction on how to implement TrueAutomation into Java/Maven project.
To get started, there should be a fully configured and working Java/Maven project. If you do not have such a project, you can [clone our sample project from Github](https://github.com/shapovalovei/testng-example)

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

3. Create the TrueAutomation Driver by adding the following lines into `java` file:

```java
import io.trueautomation.client.driver.TrueAutomationDriver;

WebDriver driver = new TrueAutomationDriver();
```

4. Create a `trueautomation.json` file in the project root directory. Name of the project should be set inside of the json file to bind it with a project in your [cloud account](https://app.trueautomation.io/app/projects). See example of `name`:`value` pair below:

```json
{
  "projectName": "your-project-name"
}
```

5. Go to [Creating tests, using TrueAutomation and Java](/getting-started/creating-tests-il?id=trueautomation-with-java) and write your first test.

## Initializing Java/Gradle project

Use this section as a step-by-step instruction on how to implement TrueAutomation into Java/Gradle project.
To get started, there should be a fully configured and working Java/Gradle project. If you do not have such a project, you can [clone our sample project from Github](https://github.com/shapovalovei/gradle-example)

**And now take the following steps:**

1. Add the repositories information in the `build.gradle` file:

```gradle
repositories {
    maven {
        url "https://mvn.trueautomation.io/artifactory/trueautomation"
    }
}
```

2. Add the dependency information in the `build.gradle` file:

```gradle
dependencies {
    testImplementation group: 'io.trueautomation', name: 'trueautomation-client', version: '0.3.7'
}
```

3. Create the TrueAutomation Driver by adding the following lines into `java` file:

```java
import io.trueautomation.client.driver.TrueAutomationDriver;

WebDriver driver = new TrueAutomationDriver();
```

4. Create a `trueautomation.json` file in the project root directory. Name of the project should be set inside of the json file to bind it with a project in your [cloud account](https://app.trueautomation.io/app/projects). See example of `name`:`value` pair below:

```json
{
  "projectName": "your-project-name"
}
```

5. Go to [Creating tests, using TrueAutomation and Java](/getting-started/creating-tests-il?id=trueautomation-with-java) and write your first test.

## Initializing Ruby/Capybara project

Use this section as a step-by-step instruction on how to implement TrueAutomation into Ruby/Capybara project.
To get started, there should be a fully configured and working Ruby/Capybara project. If you do not have such a project, you can [clone our sample project from Github](https://github.com/shapovalovei/capybara-example)

**And now take the following steps:**

1. Add the following line to your `Gemfile`:

```ruby
gem 'true_automation'
```

2. Run the command:

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

7. Make the TrueAutomation DSL available:

```ruby
config.include TrueAutomation::DSL
```

8. Create a `trueautomation.json` file in the project root directory. Name of the project should be set inside of the json file to bind it with a project in your [cloud account](https://app.trueautomation.io/app/projects). See example of `name`:`value` pair below:

```json
{
  "projectName": "your-project-name"
}
```

9. Go to [Creating tests, using TrueAutomation and Capybara/RSpec](/getting-started/creating-tests-il?id=trueautomation-with-capybararspec) and write your first test.

## Initializing JavaScript/WebdriverIO project

Use this section as a step-by-step instruction on how to implement TrueAutomation into JavaScript/WebdriverIO project.
To get started, there should be a fully configured and working JavaScript/WebdriverIO project. If you do not have such a project, you can [clone our sample project from Github](https://github.com/shapovalovei/wdioV5-example.git)

**And now take the following steps:**

1. Add the required dependencies in your `package.json` file:

```json
{
  "devDependencies": {
    "trueautomation-helper": "~0.3",
    "wdio-trueautomation-service": "~0.3"
  }
}
```

2. Then you need to add the `trueautomation` service to your services array in the `wdio.conf.js` file:

```js
// wdio.conf.js
exports.config = {
  // ...
  services: ['trueautomation'],
  // ...
}
```

3. Specify the `path` in the `wdio.conf.js` file (thus, override the default path of `'/wd/hub'`):

```js
// wdio.conf.js
exports.config = {
  // ...
  path: '/',
  // ...
}
```

4. Create a `trueautomation.json` file in the project root directory. Name of the project should be set inside of the json file to bind it with a project in your [cloud account](https://app.trueautomation.io/app/projects). See example of `name`:`value` pair below:

```json
{
  "projectName": "your-project-name"
}
```

5. Go to [Creating tests, using TrueAutomation and JavaScript/WebdriverIO](getting-started/creating-tests-il?id=trueautomation-with-javascriptwebdriverio) and write your first test.
