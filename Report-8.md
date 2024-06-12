# Information Disclosure (Django debug mode enabled)

#### Description
Your website `https://stage.example.com/` is running with debug mode turned on (DEBUG = True ). One of the main features of debug mode is the display of detailed error pages. If your app raises an exception when DEBUG is True, Django will display a detailed traceback, including a lot of metadata about your environment, such as all the currently defined Django settings

#### Steps to Reproduce
1. Visit https://stage.example.com/NON_EXISTING_PATH/ > Observe the information of debugging

#### Impact

Django DEBUG mode was enabled and showed some information on some errors.I just followed the errors and finally got some sensitive system information such as configuration, API keys ,Database users ,System Directories,etc..

#### CVSS Score

https://www.first.org/cvss/calculator/3.0#CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N 
