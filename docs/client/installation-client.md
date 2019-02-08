# Install Client {docsify-ignore}
## Installing TrueAutomation Client

You should have a TrueAutomation.io account in place to be able to leverage its capabilities. If you do not have an account yet, please [register](https://app.trueautomation.io/auth/signup) one at [TrueAutomation.io](https://trueautomation.io/)

Installation process is easy and straightforward. Just follow the recommendations in the installer or refer to Documentation section in case you have any questions.

Once you run the installer, it will automatically configure PATH environment variable and will make TrueAutomation Client available from the command line. In Windows environment you might need to re-login to your system for the changes to be applied.

### Mac OS X and Linux operating system

Run the command below in your command line to install TrueAutomation Client:

```bash
curl -o- https://trueautomation.io/installer.sh | bash
```
or

```bash
wget -qO-  https://trueautomation.io/installer.sh | bash
```
![Unix](../_gif/unix.gif 'Install process')

### Windows operating system

Before installing TrueAutomation client, you need to download and install [Microsoft Visual C ++ 2015 Redistributable Update 3 RC](https://www.microsoft.com/en-us/download/details.aspx?id=52685) 

Just [download Windows installer](https://downloads.trueautomation.io/trueautomation-setup.exe), run it, and you are done!

  ![Windows](../_gif/windows.gif 'Windows installer')

## Verifying the Installation

Make sure to verify the installed content. To do so, open the command line and run the command below:

```bash
trueautomation -h
```

![Help](../_images/ta-help-output.png 'Help output')

The message above means that the installation process has been completed successfully. Next step is [setting up your first TrueAutomation project](/getting-started/project-setup.md)