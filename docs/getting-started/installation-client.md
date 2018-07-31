## Install TrueAutomation Client

So, you’ve just finished [registration](https://app.trueautomation.io/auth/signup) at the [TrueAutomation.IO](https://trueautomation.io/).

Installing TrueAutomation client is extremely easy. The installer will automatically add TrueAutomation client to your system path so that it is available in terminals.
If it is not found, please try logging out and logging back in to your system (this is particularly necessary sometimes for Windows).

### UNIX operating system

On your computer go to Terminal and install TrueAutomation Client by running this command:
```bash
curl -o- https://trueautomation.io/installer.sh | bash
```
or
```bash
wget -qO-  https://trueautomation.io/installer.sh | bash
```
![Unix](../_gif/install-unix.gif 'Install process')

### Windows operating system

Before installing TrueAutomation client, you need to download and install [Microsoft Visual C ++ 2015 Redistributable Update 3 RC](https://www.microsoft.com/en-us/download/details.aspx?id=52685) 

Just [download Windows installer](https://trueautomation.io/downloads/trueautomation-setup.exe), run it, and you are done!

  ![Windows](../_gif/install-windows.gif 'Windows installer')


## Verifying the Installation

After installing TrueAutomation client, verify the installation worked by opening a new command prompt or terminal, and checking that TrueAutomation is available:
```bash
trueautomation -h
```

![Help](../_images/ta-help-output.png 'Help output')

You have successfully downloaded and installed TrueAutomation client! Read on to learn about [setting up your first TrueAutomation project](/getting-started/project-setup.md).


## Uninstalling TrueAutomation Client
Removing the TrueAutomation Client will remove the TrueAutomation binary and all dependencies from your machine. 
### UNIX operating system
On your computer go to Terminal and uninstall TrueAutomation Client by running this command:

```
rm -rf ~/.trueautomation/
```
### Windows operating system

Uninstall using the add/remove programs section of the control panel


## Update TrueAutomation Client

On your computer go to Terminal and update TrueAutomation Client by running this command:
```bash
curl -o- https://trueautomation.io/installer.sh | bash
```
or
```bash
wget -qO-  https://trueautomation.io/installer.sh | bash
```
![Unix](../_gif/install-unix.gif 'Install process')

### Windows operating system

Just [download Windows installer](https://trueautomation.io/downloads/trueautomation-setup.exe), run it, and you are done!

  ![Windows](../_gif/install-windows.gif 'Windows installer')
