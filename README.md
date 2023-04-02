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

#### To update our package index. These commands don’t update any installed package, they just download the latest information about the packages that can be installed or upgraded.

```
In YUM it’s:

yum check-update

In APT, instead, it’s simply:

apt update

apt-get update
```

#### Upgrading a package 

```
Update the package index and every package:
 
yum update

Update only the package MY_PACKAGE:

yum update MY_PACKAGE

Apply security-related package updates:

yum update --security


Update every package:

apt upgrade

apt-get upgrade 

Update every package along with their dependencies:

apt full-upgrade

apt-get dist-upgrade

Update only the package MY_PACKAGE:

apt-get install --only-upgrade MY_PACKAGE

Apply security-related package updates:

unattended-upgrade --dry-run -d
```

#### It’s important to know that upgrading the packages along with their dependencies potentially implies uninstalling existing software and installing new software as well if this is required by the upgrade process.

#### Standard upgrade commands, on the other side, will never uninstall anything. However, differently from apt-get upgrade (which also doesn’t install anything), apt upgrade might install new software if needed.


#### Removal of a Package

```


To get rid of an installed package and possibly its dependencies in YUM we can do one of two equivalent commands:


yum erase MY_PACKAGE

yum remove MY_PACKAGE


In RHEL7 and higher, it’s possible to erase also additional unneeded packages with autoremove:

yum autoremove MY_PACKAGE


The Debian ways to delete a package instead are:


apt remove MY_PACKAGE

apt-get remove MY_PACKAGE


However, if we want to remove the package’s configuration too, completely purging the system from it, then we can exploit purge:


apt purge MY_PACKAGE

apt-get purge MY_PACKAGE
```

#### Clean up

```
Sometimes, our system will be polluted by orphaned packages, which are not needed anymore but are still occupying space.

We can remove these unwanted packages in YUM through autoremove, without any package name:

yum autoremove

This also works in the same way on Debian distributions:

apt autoremove

apt-get autoremove

```





#### To list all available security updates without installing them, run:

```

[root@ip-172-31-84-146 ~]# yum updateinfo list security all
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 0:03:46 ago on Sun 02 Apr 2023 07:33:22 AM UTC.
RHSA-2023:0340 Moderate/Sec.  bash-5.1.8-6.el9_1.x86_64
RHSA-2022:8299 Low/Sec.       curl-7.76.1-19.el9.x86_64
RHSA-2023:0333 Moderate/Sec.  curl-7.76.1-19.el9_1.1.x86_64
RHSA-2023:0335 Moderate/Sec.  dbus-1:1.12.20-7.el9_1.x86_64
RHSA-2023:0335 Moderate/Sec.  dbus-common-1:1.12.20-7.el9_1.noarch
RHSA-2023:0335 Moderate/Sec.  dbus-libs-1:1.12.20-7.el9_1.x86_64
RHSA-2023:0335 Moderate/Sec.  dbus-tools-1:1.12.20-7.el9_1.x86_64
RHSA-2022:8385 Moderate/Sec.  dhcp-client-12:4.4.2-17.b1.el9.x86_64
RHSA-2022:8385 Moderate/Sec.  dhcp-common-12:4.4.2-17.b1.el9.noarch
RHSA-2022:8361 Moderate/Sec.  e2fsprogs-1.46.5-3.el9.x86_64
RHSA-2022:8361 Moderate/Sec.  e2fsprogs-libs-1.46.5-3.el9.x86_64
```


####  To get a list of the currently installed security updates this command can be used:

```

[root@ip-172-31-84-146 ~]# yum updateinfo list security installed
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 0:12:16 ago on Sun 02 Apr 2023 07:33:22 AM UTC.
RHSA-2023:0340 Moderate/Sec.  bash-5.1.8-6.el9_1.x86_64
RHSA-2022:8299 Low/Sec.       curl-7.76.1-19.el9.x86_64
RHSA-2023:0333 Moderate/Sec.  curl-7.76.1-19.el9_1.1.x86_64
RHSA-2023:0335 Moderate/Sec.  dbus-1:1.12.20-7.el9_1.x86_64
RHSA-2023:0335 Moderate/Sec.  dbus-common-1:1.12.20-7.el9_1.noarch
RHSA-2023:0335 Moderate/Sec.  dbus-libs-1:1.12.20-7.el9_1.x86_64
RHSA-2023:0335 Moderate/Sec.  dbus-tools-1:1.12.20-7.el9_1.x86_64
RHSA-2022:8385 Moderate/Sec.  dhcp-client-12:4.4.2-17.b1.el9.x86_64
RHSA-2022:8385 Moderate/Sec.  dhcp-common-12:4.4.2-17.b1.el9.noarch
RHSA-2022:8361 Moderate/Sec.  e2fsprogs-1.46.5-3.el9.x86_64
RHSA-2022:8361 Moderate/Sec.  e2fsprogs-libs-1.46.5-3.el9.x86_64
RHSA-2023:0337 Moderate/Sec.  expat-2.4.9-1.el9_1.1.x86_64
RHSA-2023:1141 Moderate/Sec.  gnutls-3.7.6-18.el9_1.x86_64
RHSA-2023:0752 Moderate/Sec.  grub2-common-1:2.06-46.el9_1.3.noarch
RHSA-2023:0752 Moderate/Sec.  grub2-pc-1:2.06-46.el9_1.3.x86_64
RHSA-2023:0752 Moderate/Sec.  grub2-pc-modules-1:2.06-46.el9_1.3.noarch
RHSA-2023:0752 Moderate/Sec.  grub2-tools-1:2.06-46.el9_1.3.x86_64
RHSA-2023:0752 Moderate/Sec.  grub2-tools-minimal-1:2.06-46.el9_1.3.x86_64
RHSA-2023:0334 Important/Sec. kernel-5.14.0-162.12.1.el9_1.x86_64
RHSA-2023:0951 Important/Sec. kernel-5.14.0-162.18.1.el9_1.x86_64
RHSA-2023:1470 Important/Sec. kernel-5.14.0-162.22.2.el9_1.x86_64
RHSA-2022:8267 Moderate/Sec.  kernel-5.14.0-162.6.1.el9_1.x86_64
RHSA-2023:0334 Important/Sec. kernel-core-5.14.0-162.12.1.el9_1.x86_64
RHSA-2023:0951 Important/Sec. kernel-core-5.14.0-162.18.1.el9_1.x86_64
RHSA-2023:1470 Important/Sec. kernel-core-5.14.0-162.22.2.el9_1.x86_64
RHSA-2022:8267 Moderate/Sec.  kernel-core-5.14.0-162.6.1.el9_1.x86_64
RHSA-2023:0334 Important/Sec. kernel-modules-5.14.0-162.12.1.el9_1.x86_64
RHSA-2023:0951 Important/Sec. kernel-modules-5.14.0-162.18.1.el9_1.x86_64
RHSA-2023:1470 Important/Sec. kernel-modules-5.14.0-162.22.2.el9_1.x86_64
RHSA-2022:8267 Moderate/Sec.  kernel-modules-5.14.0-162.6.1.el9_1.x86_64
RHSA-2023:0334 Important/Sec. kernel-tools-5.14.0-162.12.1.el9_1.x86_64
RHSA-2023:0951 Important/Sec. kernel-tools-5.14.0-162.18.1.el9_1.x86_64
RHSA-2023:1470 Important/Sec. kernel-tools-5.14.0-162.22.2.el9_1.x86_64
RHSA-2022:8267 Moderate/Sec.  kernel-tools-5.14.0-162.6.1.el9_1.x86_64
RHSA-2023:0334 Important/Sec. kernel-tools-libs-5.14.0-162.12.1.el9_1.x86_64

```



#### Install security updates using yum utility:

```

root@ip-172-31-84-146 ~]# yum -y update --security
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 0:02:22 ago on Sun 02 Apr 2023 07:48:11 AM UTC.
Dependencies resolved.
================================================================================================
 Package                     Arch    Version                  Repository                   Size
================================================================================================
Installing:
 kernel                      x86_64  5.14.0-162.22.2.el9_1    rhel-9-baseos-rhui-rpms     1.9 M
 kernel-core                 x86_64  5.14.0-162.22.2.el9_1    rhel-9-baseos-rhui-rpms      46 M
 kernel-modules              x86_64  5.14.0-162.22.2.el9_1    rhel-9-baseos-rhui-rpms      34 M
Upgrading:
 bash                        x86_64  5.1.8-6.el9_1            rhel-9-baseos-rhui-rpms     1.7 M
 curl                        x86_64  7.76.1-19.el9_1.1        rhel-9-baseos-rhui-rpms     299 k
 dbus                        x86_64  1:1.12.20-7.el9_1        rhel-9-baseos-rhui-rpms     8.0 k
 dbus-common                 noarch  1:1.12.20-7.el9_1        rhel-9-baseos-rhui-rpms      18 k
 dbus-libs                   x86_64  1:1.12.20-7.el9_1        rhel-9-baseos-rhui-rpms     155 k
 dbus-tools                  x86_64  1:1.12.20-7.el9_1        rhel-9-baseos-rhui-rpms      56 k
 dhcp-client                 x86_64  12:4.4.2-17.b1.el9       rhel-9-baseos-rhui-rpms     794 k
 dhcp-common                 noarch  12:4.4.2-17.b1.el9       rhel-9-baseos-rhui-rpms     131 k
 e2fsprogs                   x86_64  1.46.5-3.el9             rhel-9-baseos-rhui-rpms     1.0 M
 e2fsprogs-libs              x86_64  1.46.5-3.el9             rhel-9-baseos-rhui-rpms     225 k

```


#### yum update --security 

```

Will update any package that have at least one errata to the latest available version.

```

#### Meanwhile :


#### yum update-minimal --security

```

Will update any package to the exact version where the last errata is fixed / remediated.

```

#### Using –changelog option you can find out if particular security bug is fixed or not. 

```

[root@ip-172-31-84-146 ~]# rpm -q --changelog openssl
* Wed Feb 08 2023 Dmitry Belyavskiy <dbelyavs@redhat.com> - 1:3.0.1-46
- Fixed X.509 Name Constraints Read Buffer Overflow
  Resolves: CVE-2022-4203
- Fixed Timing Oracle in RSA Decryption
  Resolves: CVE-2022-4304
- Fixed Double free after calling PEM_read_bio_ex
  Resolves: CVE-2022-4450
- Fixed Use-after-free following BIO_new_NDEF
  Resolves: CVE-2023-0215
- Fixed Invalid pointer dereference in d2i_PKCS7 functions
  Resolves: CVE-2023-0216
- Fixed NULL dereference validating DSA public key
  Resolves: CVE-2023-0217
- Fixed X.400 address type confusion in X.509 GeneralName
  Resolves: CVE-2023-0286
- Fixed NULL dereference during PKCS7 data verification
  Resolves: CVE-2023-0401

* Thu Jan 05 2023 Dmitry Belyavskiy <dbelyavs@redhat.com> - 1:3.0.1-45
- Refactor OpenSSL fips module MAC verification
  Resolves: rhbz#2158413
- Disallow SHAKE in RSA-OAEP decryption in FIPS mode
  Resolves: rhbz#2144011

* Wed Nov 30 2022 Clemens Lang <cllang@redhat.com> - 1:3.0.1-44.1
- Fix explicit indicator for PSS salt length in FIPS mode when used with
  negative magic values
  Resolves: rhbz#2144013
- Update change to default PSS salt length with patch state from upstream 
  Related: rhbz#2144013

* Mon Nov 14 2022 Dmitry Belyavskiy <dbelyavs@redhat.com> - 1:3.0.1-44
- SHAKE-128/256 are not allowed with RSA in FIPS mode
  Resolves: rhbz#2144010
- Avoid memory leaks in TLS
  Resolves: rhbz#2144008
- FIPS RSA CRT tests must use correct parameters
  Resolves: rhbz#2144006
- FIPS-140-3 permits only SHA1, SHA256, and SHA512 for DRBG-HASH/DRBG-HMAC
  Resolves: rhbz#2144017
- Remove support for X9.31 signature padding in FIPS mode
  Resolves: rhbz#2144015
```



