# TrueAutomation commands {docsify-ignore}

## Starting TrueAutomation client
You can start the TrueAutomation client, using the command: ````trueautomation```` or ````trueautomation start````. The client will be started with default parameters.

 Syntax:
```bash
trueautomation [options]
trueautomation start [options]
```

 Options:

| Options | Example | Description |
| --- | --- | --- |
| -v, --version             	| trueautomation -v, <br>trueautomation --version                       	| output the client version number                        	|
| --port                    	| trueautomation start --port 9515                                 	| port to listen on                                       	|
| --driverPort              	| trueautomation start --driverPort 4444                           	| port for driver to listen on                            	|
| --log-file                	| trueautomation start --log-file ~/logs.txt                       	| starting the client with writing logs into the log-file 	|
| --driver <br> --driver-version| trueautomation start --driver chromedriver <br> --driver-version 2.41 	| setting driver name and version                         	|
| --remote                  	| trueautomation start --remote                                    	| do not run default driver                               	|
| -h, --help                	| trueautomation -h, <br>trueautomation --help                          	| output usage information                                	|


## Project initialization
Run the command ```trueautomation init | i``` to initialize a new or existing project.

 Syntax:
```bash
trueautomation init
trueautomation i
```
## Setting API Key
Use the command ````trueautomation api-key```` to set a new API key.

 Syntax:
```bash
trueautomation api-key [api-key]
```
## Drivers management
Currently, we support all major drivers: Chrome Driver, Gecko Driver, Microsoft Web Driver (Edge Driver), Safari Driver and Remote Driver functionality. Use the following driver names to manage this drivers:

```bash
chromedriver, geckodriver, microsoftwebdriver, safaridriver
```
Use the command to download the driver version you need:
```trueautomation driver download```.

 Syntax:
```bash
trueautomation driver download [driver_name] [version]
```

 Example:
```bash
trueautomation driver download chromedriver 2.41
```
You can see the downloaded drivers list, using the command: ```trueautomation driver list```.

 Syntax:
```bash
trueautomation driver list
```
There is the command to set default driver: ````trueautomation driver use````.

 Syntax:
```bash
trueautomation driver use [driver_name] [version]
```

 Example:
```bash
trueautomation driver use geckodriver 0.21.0
```
Use the command to remove a some driver: ```trueautomation driver remove```.

 Syntax:
```bash
trueautomation driver remove [driver_name] [version]
```

 Example:
```bash
trueautomation driver remove geckodriver 0.21.0
```
You can update all drivers to the latest version, using the following command:
```trueautomation driver update all```.

 Syntax:
```bash
trueautomation driver update all
```
For more information about drivers management, use the option:

| Option | Example | Description |
| --- | --- | --- |
|-h, --help|           trueautomation driver -h, <br>trueautomation driver --help  | output usage information  |


## Starting TrueAutomation IDE mode
To start using the TrueAutomation integrated development environment (IDE), run the command ```trueautomation ide``` for your project.

 Syntax:
```bash
trueautomation ide
```
