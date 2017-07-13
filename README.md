# TEMPLATE: CODE TITTLE // Ex: AddCdnHost
Here we give a brief explanation of the code (No longer than 1 paragraph) // Ex:

The API AddCdnHost will allow for users to add CDN domains into their consoles. This is very useful as, by only switching some fields into this code, a CDN will be created and activated into the user's console. Please note that this process can be realized in two very different ways, one by using the interface in the console and another by running the API.

## The Basics
In here we will describe the pre-requisites needed to run the program, as softwares, packages... // Ex:

As this is a Tencent Cloud API, the follow pre-requisites will be needed in your PC to be able to run

*Alternative to this may be to upload a polished word or pdf file with the instructions

### Pre-requisites
Here a list of pre-requisites will be given. This list will include programs, packages... with links and steps to download them correctly

**Please note that these pre-requisites are only necessary if process is going to be realized by running the API, if it is going to be added trhough the UI please skip this section and go to "Adding the CDN Host"**

This API runs in Python 2.7, therefore Python 2.7 will be needed
  - For more flexibility, please add Python to the PATH
  - Download link: https://www.python.org/downloads/windows/
  
A program to un-zip files will be neccesary, it is recommended to use 7-ZIP
  - Download link: http://www.7-zip.org/download.html

An editor will be required to edit python code files, it is recommended to use Note ++ 
  - Download link: https://notepad-plus-plus.org/ 

Follow the next steps to install Python Package “Requests” (HTTP for Humans):
  1.  Download version 0.10.6 from https://pypi.python.org/pypi/requests/0.10.6#downloads 
  2.  Extract files from *“requests-0.10.6.tar.gz”*
  3.	Open file with 7_Zip, then open folder “requests-0.10.6”
  4.	Next step is to open the folder “dist”
  5.	Inside “dist”, another folder named “requests-0.10.6” will be found
  6.	Use 7-Zip to extract this folder
  7.	Suggest location: “C:\mytools\Python\requests-0.10.6”
  8.  Change directory (if necessary) and run 
  ```
  “python setup.py install”
  ```
  9.  If installation is succesful, output will be: 
  ```
  Installed c:\users\.....
  Finished processing dependencies for requests==0.10.6
  ```
  ## Action that program will do (if multiple ways, describe all possible ways) // Ex: Adding the CDN host
Adding a CDN host can be done in two different ways, however both of them will work identically:

  ### Adding a CDN host trhough the interface in the console
  1. Access the console
  2. Click on "Cloud Products" > "CDN"
  3. Go to "Domain Management"
  4. Click on "Create a distribution"
  5. Complete all the required fields and press "Submit"
  6. Done! Your CDN will be set in the following 5 minutes!
  
  ### Adding a CDN host trhough the API
  To add a CDN trhough the API please take in consideration the following documentation
    - Link: https://www.qcloud.com/document/api/228/1406
  Please, follow the code below and replace the parameters in the field with the user's parameters

```
#!/usr/bin/python
#-*- coding: utf-8 -*-

from src.QcloudApi.qcloudapi import QcloudApi

module = 'cdn'
action = 'AddCdnHost'
config = {
    'Region': 'gz',
    'secretId': 'Replace this string with User's ID',
    'secretKey': 'Replace this string with User's Key',
    'method': 'post'
}

params = {
    "host" : 'Replace this string with name of acceleration domain',
    "projectId": 0,
    "hostType": "cname",                    #Note: If you select FTP, you do not need to enter origin server configurations
    "origin": "Replace this string with origin configuration",
    "fwdHost": "Replace this string with Forward Host",
    "serviceType": "web"
}

try:
    service = QcloudApi(module, config)
    print service.generateUrl(action, params)
    print service.call(action, params)
except Exception, e:
    print 'exception:', e
```

   #### Output
   - If added successfully:
   ```
   "code": 0,
   "message": "",
   "codeDesc": "Success"
   ```
   - If addittion failed:
   ```
    "code": 4000,
    "message": "(20004) Not filed cdn audit no icp [cdn audit no icp [The current domain has not been filed with MIIT for the record]]",
    "codeDesc": 20004
   ```
