# Easy Setup 

1. Register an account with TrueAutomation at https://app.trueautomation.io/auth/signup
2. On your computer go to Terminal and install TrueAutomation Client by running this command: 

    _True Automation client requires [Node v9+](https://nodejs.org/en/) to run. The best way to get proper up-to-date and stable environment is install node via nvm. 
    So we suggest to to install nvm for your platform first. Please follow instructions [here](https://github.com/creationix/nvm). 
    Once you have nvm in place, the latest version of node can be installed. Run this command to do so:_

    2.1. Unix operating system 
 
   ```bash
    curl -o- https://trueautomation.io/installer.sh | bash
   ```
   or 
   ```bash
    wget -qO-  https://trueautomation.io/installer.sh | bash
   ```
   
   2.2. Windows operating system
   
   ?> _TODO:_ add setup process on Windows
  
3. Select programming language (currently supported languages: Ruby and Java)

    3.1. Ruby
    
    _TrueAutomation client requires Ruby 2.2.0 or later to run. We suggest to get the proper version or Ruby [here](https://www.ruby-lang.org/en/documentation/installation/).
     We are also supporting Capybara framework. If you prefer to work with it we suggest you to get it [here](https://github.com/teamcapybara/capybara).
      If you will need RSpec, you can get it [here](http://rspec.info/documentation/)._
         
    3.2. Java
    
   _TrueAutomation client requires JDK 8 or later. We suggest to get the proper version of JDK [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
    You will also need Maven to work with your projects and run the tests. We suggest you to get the proper version of Maven [here](https://maven.apache.org/install.html)._
    
    

   