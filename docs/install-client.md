# Install TrueAutomation Client

So, you’ve just finished [registration](https://app.trueautomation.io/auth/signup) at the [TrueAutomation.IO](https://trueautomation.io/).

Installing TrueAutomation client is extremely easy. The installer will automatically add TrueAutomation client to your system path so that it is available in terminals.
If it is not found, please try logging out and logging back in to your system (this is particularly necessary sometimes for Windows).

## UNIX operating system

On your computer go to Terminal and install TrueAutomation Client by running this command:
```bash
curl -o- https://trueautomation.io/installer.sh | bash
```
or
```bash
wget -qO-  https://trueautomation.io/installer.sh | bash
```
![Unix](_gif/install-unix.gif 'Install process')

## Windows operating system

### Installation using installer

If you are on Windows, there is a great project to help you install TrueAutomation: [TrueAutomation installer](https://trueautomation.io/downloads/trueautomation-setup.exe). 
It gives you everything you need to set up a full TrueAutomation environment on Windows.

Just [download it](https://trueautomation.io/downloads/trueautomation-setup.exe), run it, and you are done!

  ![Windows](_gif/install-windows2.gif 'Windows installer')
### Manual installation

1. [Download executable](https://trueautomation.io/downloads/trueautomation-win.exe)
2. Create a new folder named `ta` in `C:\` and move executable to this folder

  ![Windows executable](_images/windows-executable.png 'Windows executable')
3. Set new environment variable `TRUEAUTOMATION_EXEC` to point to the executable

    - From the desktop, right click the Computer icon.
    - Choose Properties from the context menu.
    - Click the Advanced system settings link.
    - Click Environment Variables button.
    - Click New... button.
    - Fill variable data.
    - Click OK.

  ![New variable](_images/new-var.png 'New variable')
4. Add path to `trueautomation.exe` binary to your `PATH` variable

  ![Update PATH](_images/update-path-var.png 'Update PATH')
5. Close all remaining windows by clicking OK.
6. Reopen Command prompt window.

## Verifying the Installation

After installing TrueAutomation client, verify the installation worked by opening a new command prompt or terminal, and checking that TrueAutomation is available:
```bash
trueautomation -h
```

![Help](_images/ta-help-output.png 'Help output')

You have successfully downloaded and installed TrueAutomation client! Read on to learn about [setting up your first TrueAutomation project](project-setup.md).
