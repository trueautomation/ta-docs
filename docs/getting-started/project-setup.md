# Project Setup

TrueAutomation client has a built-in command for initializing a project in which TrueAutomation should be used: `trueautomation init`.

**You can use this guide as step-by-step instructions to initialize a project using your command line!**

1. If you already have a folder where your project should be located - please go to it. E.g. :

```bash
cd my-project/
```

Or create a new folder for your project and proceed to it. E.g. :

```bash
mkdir my-project
```

2. Run command to initialize your project. E.g. :

```bash
trueautomation init
```

3. If you’re running TrueAutomation for the 1st time, you will be asked whether you have an account with [TrueAutomation.io](https://trueautomation.io)

    3.1. If you have an account - enter `y` in the command line. You will be prompted to the next step.

    3.2. If you do not have an account - enter `n` in the command line. In this case you will need to register an account with TrueAutomation.io at: https://app.trueautomation.io/auth/signup and then return back to initialization process.

4. Enter your API key. You can get it in your profile at TrueAutomation.io account:

    ![API key](../_gif/api-500-sp.gif 'API key')

5. The TrueAutomation app will detect whether the folder of the project is empty or not.

    5.1. If you initialize the project in an empty directory, you will see this message:
    
    ![Technology stack](../_images/technology.png 'Technology stack')
    
    Use arrows on your keyboard to choose a technology stack you are planning to use!
    
    5.2. TrueAutomation app will offer to update your project if you initialize it in the directory that already contains a supported framework.
    
    > ? We detected that your project is based on Java/Maven. Do you want to update the project with TrueAutomation? (Y/n)
    
    Choose `Y` to update the project. We will modify your project and you will be able to use it with TrueAutomation.
    
    ![Congratulations](../_images/congrat-update.png 'Congratulations')
    
    If you are not ready to update your project, choose `n`. The initialization process will be interrupted. You can return to the initialization process by using command `trueautomation init` again.
    
    ![Interrupted](../_images/interrupted.png 'Interrupted')
   
6. You will be asked whether you have a project created at your TrueAutomation.io account. This is needed to make the most of TrueAutomation experience.

    > ? Do you want to use existing (e) TrueAutomation.IO project or create a new one (c)? (Ech)
    
    Enter `e` (existing) to use an existing project from your TrueAutomation.io account. You will be asked to choose the project name from the list.
    
    ![Existing project](../_images/use-existing-project.png 'Existing project')
    
    If you do not have a necessary project in your TrueAutomation.io account, please enter `c` (create) to create one right away.
    
    ![New project](../_images/use-new-project.png 'New project')

7. Your initialization process is almost over.

    7.1. If you have initialized project in an empty directory you will see the message like that:
    
    ![Java/Maven congratulations](../_images/java-congratulations.png 'Java/Maven congratulations')
    
    7.2. If you initialized an existing project, you will see the message:
    
    ![Congratulations](../_images/congrat-update.png 'Congratulations')

Congratulations. You’re good to go with TrueAutomation. If you have suggestions or questions reg this guide - let us know at [team@trueautomation.io](mailto:team@trueautomation.io)

![Initial process](../_gif/init-ta.gif 'Initial process')
