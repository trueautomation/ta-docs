# Initializing project

##### To initialize project:
1. Go to terminal
2. If you already have a folder where your project should be located - please go to it. E.g. : 
```bash
cd my-project/
```
Or create a new folder for your project. E.g. : 
```bash
mkdir my-project
```
3. Run command to initialize your project. E.g. : 
```bash
trueautomation init
```
4. If you’re running TrueAutomation for the 1st time, you will be asked whether you have an account with TrueAutomation.
    
    4.1. If you have an account - enter `y` in the terminal. You will be prompted to the next step.

     _If you do not have an account - enter `n` in the terminal. In this case you will need to register an account with TrueAutomation at: https://app.trueautomation.io/signup and then return back to step 3 of initialization process._
     
    4.2. Enter you API key in the terminal. You can get your API key in your account of TrueAutomation at https://app.trueautomation.io/app/profile
5. The TrueAutomation app will detect whether the folder of the project is empty or not.
    
    5.1. Directory is empty. You will get a message:
    
    > Directory is empty. Do you want to initialize a new project? (у/n)

    If you enter `y`,  you will be prompted to a selection of technology:
    
    ![Technology stack](_images/technology-stack.png 'Technology stack')
    
    Please choose a technology stack you’re planning to use.

    If you enter `n`, initialization of the project will be aborted.
    
    5.2. If the directory is not empty. TrueAutomation app will confirm the technology with you.

    > E.g.: We detected that your project is based on Capybara. Please confirm that (y/n).
   
    If the technology was detected correctly, please enter `y` and you will be prompted to the next step.

    If the technology was detected in a wrong way, please enter `n`. The initialization will be aborted. Please let us know at [team@trueautomation.io](mailto:team@trueautomation.io) about such case and we will look into it ASAP.

6. You will be asked whether you have a project created at your TrueAutomation account. This is needed to make the most of TrueAutomation experience.
   
   > E.g.: Do you want to use existing (e) TrueAutomation.IO project or create a new one (c)? (Ech) (e/c)

    If you already have this project created - enter `e`. You will be asked to provide the name of the project as it is stated in your TrueAutomation account.
    
    ![Existing project](_images/existing-project.png 'Existing project')
    
    If you do not have this project in your TrueAutomation account, please enter `c` and you will be suggested to create one right away:
    
    ![New project](_images/new-project.png 'New project')

7. Your initialization process is almost over.
   
    7.1. If you have initialized project in an empty directory. You will see the message like that:
     
     * Ruby/Capybara
          
     ![Capybara congratulations](_images/capybara-congratulations.png 'Capybara congratulations')
     
     * Ruby without additional frameworks
     
     ?> _TODO:_ add image with congratulations message
     
     * Java/TestNG
     
     ?> _TODO:_ add image with congratulations message
     
    7.2 If your project was initialized in the folder that already contained framework - you should see this message

     ![Congratulations](_images/congratulations.png 'Congratulations')
     
Congratulations. You’re good to go with TrueAutomation. If you have suggestions or questions reg this guide - let us know at [team@trueautomation.io](mailto:team@trueautomation.io) 


 ![Initial process](_gif/init-ta.gif 'Initial process')