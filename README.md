## Pre-requisite for Load test execution from python script:
* Linux Machine
* Python3
* Python external module dependancies
	* schedule
	* psycopg2

## Jmeter setup:
	Download and extract jmeter setup to location : '/home/PT/tools/jmeter/' 
	2. Download [cmdrunner](https://repo1.maven.org/maven2/kg/apc/cmdrunner/2.2/cmdrunner-2.2.jar)  download to /home/PT/tools/jmeter/<jmeter_version>/lib
	3. Download [plugin-manager](https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-manager/1.6/jmeter-plugins-manager-1.6.jar) download to /home/PT/tools/jmeter/<jmeter_version>/lib/ext

	4. Run command `java -cp /home/PT/tools/jmeter/<jmeter_version>/lib/ext/jmeter-plugins-manager-1.6.jar org.jmeterplugins.repository.PluginManagerCMDInstaller`

	5. Run Command `sh /home/PT/tools/jmeter/<jmeter_version>/bin/PluginsManagerCMD.sh install jpgc-dummy=0.4`
	
	6. Verify if 'ls /home/PT/tools/jmeter/<jmeter_version>/lib/ext/jmeter-plugins-dummy-0.4.jar' exist.


## Steps to Execute Performance Test:
* Pull project from git
	1. `mkdir sample-project` 
	2. `cd sample-project` # this is your project path
	3. `git init`
	4. `git remote add origin "git@gitlab.connectwisedev.com:qa/performance-engineering.git"`
	5. `git checkout -b sample-project`
	6. `git pull origin sample-project`
* To Run from local machine (Windows Machine)- **This Step is not required to perform in LG machine.**
	* Update *projectpath* in Jmeter TestPlan with project path and run the test.
	* **Dont Run test from Local machine**
* To Execute load test from LG machine (Linux machine) follow the below steps.
	* set config/config.json 
		* As mentioned in [Config file section](https://confluence.connectwisedev.com/display/QA/Documentation+for+Performance+Automation+by+Python)
	* Change Execution related  parameter like users, rammup, execution duration.
		* In `config.json` modify the values of *projectpath* and *JMETER_HOME*
	* Execute the test
		```Python
		/<Projectpath>/scripts/performanceAutomation.py /<projectpath>/config/config.json <build number>
		```
	* Monitor the logs <project path>/logs/loadtest.logs and jmeter_loadtest.log
	* Once the test is completed in loadtest.logs you will get path of performance result file 