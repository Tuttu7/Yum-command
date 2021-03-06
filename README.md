#### YUM (Yellowdog Updater Modified) is an open-source command-line as well as graphical-based package management tool for RPM (RedHat Package Manager) based Linux systems.

#### Use the list function to search for the specific package with a name

```
[root@ip-172-31-26-143 ~]# yum list vsftpd
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Installed Packages
vsftpd.x86_64                       3.0.2-25.amzn2             
```

#### To update a package :

```
[root@ip-172-31-26-143 rpm]# yum update vsftpd
```


#### To downgrade a package

```
root@ip-172-31-26-143 ~]# yum -y downgrade  vsftpd


root@ip-172-31-26-143 ~]# yum list vsftpd
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Existing lock /var/run/yum.pid: another copy is running as pid 3523.
Another app is currently holding the yum lock; waiting for it to exit...
  The other application is: yum
    Memory : 162 M RSS (381 MB VSZ)
    Started: Sat Jun  4 06:07:58 2022 - 00:05 ago
    State  : Running, pid: 3523
Installed Packages
vsftpd.x86_64                     3.0.2-22.amzn2.0.1                     @amzn2-core
Available Packages
vsftpd.x86_64                     3.0.2-25.amzn2      
```



#### Installing Yum plugin to lock specified packages from being updated. This allows you to protect packages from being updated by newer versions.

```
[root@ip-172-31-26-143 ~]# yum install yum-plugin-versionlock


[root@ip-172-31-26-143 ~]# yum versionlock list
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
versionlock list done
```

#### To add a package to version lock list 

```
[root@ip-172-31-26-143 ~]# yum versionlock add vsftpd
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
Adding versionlock on: 0:vsftpd-3.0.2-22.amzn2.0.1
versionlock added: 1
```

#### To view the version lock list 

```
[root@ip-172-31-26-143 ~]# yum versionlock list
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
0:vsftpd-3.0.2-22.amzn2.0.1.*
versionlock list done


[root@ip-172-31-26-143 ~]# yum -y downgrade vsftpd
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
amzn2-core                                                   | 3.7 kB  00:00:00     
Nothing to do
```

#### To delete the package from version lock list 

```
[root@ip-172-31-26-143 ~]# yum versionlock delete vsftpd
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
Deleting versionlock for: 0:vsftpd-3.0.2-22.amzn2.0.1.*
versionlock deleted: 1
```


#### To view yum history 

```
[root@ip-172-31-26-143 ~]# yum history list
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
ID     | Command line             | Date and time    | Action(s)      | Altered
-------------------------------------------------------------------------------
     3 | install yum-plugin-versi | 2022-06-04 06:09 | Install        |    1   
     2 | -y downgrade vsftpd      | 2022-06-04 06:07 | Downgrade      |    1   
     1 | -y install vsftpd        | 2022-06-04 06:07 | Install        |    1   
history list

```



#### To view all packages installed in the system

```

[root@ip-172-31-26-143 rpm]# yum list installed | less

Loaded plugins: extras_suggestions, langpacks, priorities, update-motd,
              : versionlock
Installed Packages
GeoIP.x86_64                          1.5.0-11.amzn2.0.2               installed
PyYAML.x86_64                         3.10-11.amzn2.0.2                installed
acl.x86_64                            2.2.51-14.amzn2                  installed
acpid.x86_64                          2.0.19-9.amzn2.0.1               installed
amazon-linux-extras.noarch            2.0.1-1.amzn2                    installed
amazon-linux-extras-yum-plugin.noarch 2.0.1-1.amzn2                    installed
amazon-ssm-agent.x86_64               3.1.1188.0-1.amzn2               installed
at.x86_64                             3.1.13-24.amzn2                  installed
attr.x86_64                           2.4.46-12.amzn2.0.2              installed
audit.x86_64                          2.8.1-3.amzn2.1                  installed
audit-libs.x86_64                     2.8.1-3.amzn2.1                  installed

```


#### To know the information about a package before installing it. To get information on a package just issue the below command.

```

[root@ip-172-31-26-143 rpm]# yum info vsftpd
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
Installed Packages
Name        : vsftpd
Arch        : x86_64
Version     : 3.0.2
Release     : 25.amzn2
Size        : 345 k
Repo        : installed
From repo   : amzn2-core
Summary     : Very Secure Ftp Daemon
URL         : https://security.appspot.com/vsftpd.html
License     : GPLv2 with exceptions
Description : vsftpd is a Very Secure FTP daemon. It was written completely from
            : scratch.
```


#### To list all the available packages in the Yum database, use the below command.


```

[root@ip-172-31-26-143 rpm]# yum list | less

```



#### To view all the past transactions of the yum command, just use the following command.

```
[root@ip-172-31-26-143 ~]# yum history info 
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
Transaction ID : 3
Begin time     : Sat Jun  4 06:09:05 2022
Begin rpmdb    : 451:c01f9b290c2fce495c5d7dfc9c58889f629ee38f
End time       :            06:09:06 2022 (1 seconds)
End rpmdb      : 452:3522979bae7a05d0d792e038a0e800cc40069991
User           : EC2 Default User <ec2-user>
Return-Code    : Success
Command Line   : install yum-plugin-versionlock
Transaction performed with:
    Installed     rpm-4.11.3-48.amzn2.0.2.x86_64 installed
    Installed     yum-3.4.3-158.amzn2.0.5.noarch installed
Packages Altered:
    Install yum-plugin-versionlock-1.1.31-46.amzn2.0.1.noarch @amzn2-core
history info
```

#### To view all information about a specific transaction / event :


```
[root@ip-172-31-26-143 ~]# yum history info 3
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd, versionlock
Transaction ID : 3
Begin time     : Sat Jun  4 06:09:05 2022
Begin rpmdb    : 451:c01f9b290c2fce495c5d7dfc9c58889f629ee38f
End time       :            06:09:06 2022 (1 seconds)
End rpmdb      : 452:3522979bae7a05d0d792e038a0e800cc40069991
User           : EC2 Default User <ec2-user>
Return-Code    : Success
Command Line   : install yum-plugin-versionlock
Transaction performed with:
    Installed     rpm-4.11.3-48.amzn2.0.2.x86_64 installed
    Installed     yum-3.4.3-158.amzn2.0.5.noarch installed
Packages Altered:
    Install yum-plugin-versionlock-1.1.31-46.amzn2.0.1.noarch @amzn2-core
history info
```



### To undo the change ( revert changes )

```
[root@ip-172-31-26-143 ~]# yum history undo 3
```


#### To redo the changes ( Do it once again )

```
[root@ip-172-31-26-143 ~]# yum history redo 3
```


#### To keep your system up-to-date with all security and binary package updates, run the following command. It will install all the latest patches and security updates to your system.

```
[root@ip-172-31-26-143 rpm]# yum update

```


#### To find how many installed packages on your system have updates available, check to use the following command.

```
[root@ip-172-31-26-143 rpm]# yum check-update
```


