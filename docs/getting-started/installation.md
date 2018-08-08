# Install Client {docsify-ignore}
## Installing TrueAutomation Client {docsify-ignore}

So, you’ve just finished [registration](https://app.trueautomation.io/auth/signup) at the [TrueAutomation.IO](https://trueautomation.io/).

Installing TrueAutomation client is extremely easy. The installer will automatically add TrueAutomation client to your system path so that it is available in terminals.
If it is not found, please try logging out and logging back in to your system (this is particularly necessary sometimes for Windows).

### UNIX operating system {docsify-ignore}

On your computer go to Terminal and install TrueAutomation Client by running this command:
```bash
curl -o- https://trueautomation.io/installer.sh | bash
```
or
```bash
wget -qO-  https://trueautomation.io/installer.sh | bash
```

![Unix](../_gif/unix.gif 'Install process')

### Windows operating system {docsify-ignore}

Before installing TrueAutomation client, you need to download and install [Microsoft Visual C ++ 2015 Redistributable Update 3 RC](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

Just [download Windows installer](https://trueautomation.io/downloads/trueautomation-setup.exe), run it, and you are done!

![Windows2](docs/_gif/windows.gif 'Windows installer')


## Verifying the Installation {docsify-ignore}

After installing TrueAutomation client, verify the installation worked by opening a new command prompt or terminal, and checking that TrueAutomation is available:
```bash
trueautomation -h
```

![Help](../_images/ta-help-output.png 'Help output')

You have successfully downloaded and insta
