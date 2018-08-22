# Initializing automatically

There are two ways for you to start writing tests with TrueAutomation:

* To initialize a project with automatic tests using TrueAutomation Client and built-in command:  (for details checkout the [Project Setup](/getting-started/project-setup.md)).

    ```bash
    mkdir my-project
    cd my-project
    trueautomation init
    ```

    Choose your technology stack with numbers 1) Capybara/RSpec or 2) Java/Maven

    Select existing project or new one

    Run your test with
    ```bash
        mvn -Dtest=exampleTest test
    ```




   This way is the easiest. You can initialize a project from scratch. We generate a sample project for you or you can update your own exciting project.


   ![Initial process](../_gif/init-ta.gif 'Initial process')



* To initialize a project with tests [manually](/initializing/initializing-manually.md).
