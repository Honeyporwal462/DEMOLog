1. Download Python 3, see [Python 3 Installation & Setup Guide in Windows and Linux environment](https://realpython.com/installing-python/)

2. To install the necessary dependency packages, create a virtual environment and activate that environment, then use the install from [CA_Spectrum-Packages-Requirements.txt](CA_Spectrum-Packages-Requirements.txt) command, see [Creating virtual environment and managing packages with pip](https://docs.python.org/3/tutorial/venv.html)

>Below code block is a reference from Windows platform
```
#Lets assume that you have C:\Spectrum directory
C:\> cd C:\Spectrum
#Check whether python is installed
C:\Spectrum>python --version
Python 3.7.2

#Create a virtual environment
C:\Spectrum>python -m venv spectrum_venv
#Activate the environment
C:\Spectrum>spectrum_venv\Scripts\activate.bat
#Install packages from CA_Spectrum-Packages-Requirements.txt
(spectrum_venv)C:\Spectrum>pip install -r CA_Spectrum-Packages-Requirements.txt
```

>Below code block is a reference from Linux(CentOS-7.8) platform
```
#Let’s assume that you have Spectrum directory
[/]$ cd /Spectrum

#Check whether python is installed
[/Spectrum]$ python3 --version
Python 3.7.2

#Create a virtual environment
[/Spectrum]$ python3 -m venv spectrum_venv
#Activate the environment
[/Spectrum]$ source spectrum_venv/bin/activate
#Install packages from CA_Spectrum-Packages-Requirements.txt
(spectrum_venv) [/Spectrum]$ pip3 install -r CA_Spectrum-Packages-Requirements.txt
```
>Note: Before downloading Client-Side Wrappers, login to [Platform DXC's Package Repository](https://artifactory.platformdxc-mg.com/) with DXC Global Pass credentials.  So that it won't prompt you for credentials. 

3. Download [Client-Side Wrappers](https://github.dxc.com/Platform-DXC/hybrid-wrapper/tree/master/src/ca_spectrum/client-side-wrapper) and unzip it in the same location where virtual environment(spectrum_venv) is set up.

4. Refer [config.yaml](https://github.dxc.com/Platform-DXC/hybrid-wrapper/tree/master/src/ca_spectrum/client-side-wrapper/config.yaml) Wrapper script contains config.yaml which is used to configure severity mapping, incident category mapping and log file location.So update this file as per as client need.
> In severity mapping, key refers to CA OneClick Server severities and value refers to PDXC severities.<br>
> in Incident category, Mapping key refers to alert title and values refers to PDXC incident category. It also contains a default value which will be used if alert title will not present in it.<br>
> logfiledirectory used to provide the log file location. If it's not define then the log file will be created in the same location where scripts are present.

5. Execute SpectrumPdxcSetup script for generating key file, configuration file and initialization file to be used by SpectrumPdxcEventWrapper.py script to use when sending event information from the CA OneClick Server to the PDXC API gateway.
>Setup file can be executed once and can be re-used.

>Windows platform
```
(spectrum_venv) C:\Spectrum> python3 SpectrumPdxcSetup.py
```
>Linux platform
```
(spectrum_venv) [/Spectrum]$ python3 SpectrumPdxcSetup.py
```
6. The setup script will prompt for the items listed at the beginning of this section.

>Below code block is a reference from Linux platform
```
(spectrum_venv) [/Spectrum]$ python3 SpectrumPdxcSetup.py
-----------Provide spectrum details----------
Enter the CA OneClick Server IP Address : 3.23.59.138
----------Provide spectrum api credentials----------
Enter your CA OneClick Server port number - [default:80]: 8080
Enter the Wrapper instance or Fully Qualified Domain Name(FQDN) of CA OneClick Server: Spectrum_FQDN
Enter the username for spectrum api access : spectrum_user1
Enter the password for spectrum api access : ********

NOTE: You can configure for PDXC environments listed here: devqa, globalpreprod, globalprod, uspreprod, usprod
----------Provide PDXC API Environment----------
Enter the PDXC Environment : devqa
----------Provide PDXC API credentials----------
Enter the username for PDXC API access: pdxc_events_user1
Enter the password for PDXC API access: **********
----------Provide registered event category name----------
Make sure to provide registered event category name present in PDXC ServiceNow.
Enter the registered event category name in PDXC ServiceNow  : _CategoryName_
----------Provide domain name----------
Make sure to provide registered customer domain name as it will help to ensure the incidents end up in the appropriate locations in PDXC ServiceNow.
Enter the customer registered domain name in PDXC ServiceNow  : _DomainName_

Successfully created aesKey.yaml, credentials.yaml, init.yaml files
```
7. To run SpectrumPdxcEventWrapper file in the backgorund use below command :-
```
(spectrum_venv) [/Spectrum]$ python3 SpectrumPdxcEventWrapper.py &
```
8. To auto start your SpectrumPdxcEventWrapper.py file during Server Restart ,go to crontab and add below command:
```
(spectrum_venv) [/Spectrum]$ crontab -e
@reboot cd /Spectrum/ && $(which python3) SpectrumPdxcEventWrapper.py &
```
>Note: Pass the SpectrumPdxcEventWrapper.py file path and python3 executable path of virtual environment as arguments in the above crontab entry. In my example, the SpectrumPdxcEventWrapper.py file is located at /Spectrum Directory.\
>Note: If you want to stop execution of SpectrumPdxcEventWrapper.py ,check the Process id and then kill it.See below example.
```
(spectrum_venv) [/Spectrum]$ ps -ef |grep SpectrumPdxcEventWrapper.py
Spectrum      2746  2430  1 10:04 pts/0    00:00:00 python3 SpectrumPdxcEventWrapper.py
Spectrum      2789  2430  0 10:05 pts/0    00:00:00 grep --color=auto SpectrumPdxcEventWrapper.py
(spectrum_venv) [/Spectrum]# kill -9 2746

```
