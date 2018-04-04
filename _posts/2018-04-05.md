---
layout: post
title: RHCSA-automount
---

## Introduction to autofs 

Autofs is a difficult topic for me to understand at first, now still, I understand how it works, but the justification doesn't sounds very convincing. 

Autofs is mostly used for mounting home directory, which the user may not be accessing on a very frequent basis, thus autofs can be used in so called `on demand mounting`, it is a mandatory topic on RHCSA, but still, it does't hurt to mount persistently with `/etc/fstab`. 

## Installing autofs
As the autofs is not installed by default, you might need to install it with: 
`yum install autofs -y`

## Configuring autofs for user's home directory 
Using vim to open `/etc/auto.master`, adding a new line below the first line without comment, the misc actually provides very good example for you to start. The auto.misc is the configuration file for the misc mount, similarly, we create auto.home. 
```
#
# Sample auto.master file
# This is a 'master' automounter map and it has the following format:
# mount-point [map-type[,format]:]map [options]
# For details of the format look at auto.master(5).
#
**/misc   /etc/auto.misc**
`/home/ldap /etc/auto.home`
```
To avoid affecting the local users from login in, we will not mount it on /home directly, but rather /home/ldap. In the configuration file for /etc/auto.home, we can copy the file /etc/auto.misc, the content looks like: 
```
[root@drunkpiano sssd]# cat /etc/auto.misc 
#
# This is an automounter map and it has the following format
# key [ -mount-options-separated-by-comma ] location
# Details may be found in the autofs(5) manpage

cd		-fstype=iso9660,ro,nosuid,nodev	:/dev/cdrom

# the following entries are samples to pique your imagination
**#linux		-ro,soft,intr		ftp.example.org:/pub/linux** 
```

We will below command to create home configuration file 
`cp /etc/auto.misc /etc/auto.home` 

In the file, we will add 
`*     -rw    labipa:/home/ldap/& `

The above commands mounts everything from the labipa:/home/ldap to the /home/ldap in the local directory. To mount a single user only, add the following instead: 
`ldapuser1   -rw   labipa:/home/ldap/ `

If you forgot the options especially about the &, you can get help searching & by: 
```
man 5 autofs
/& 
````

After that restart your autofs service by 
`systemctl restart autofs`

Verify that the home directory is mounted: 
```
[root@drunkpiano ~]# su - ldapuser1
Last login: Thu Apr  5 01:55:59 +08 2018 on pts/0
-sh-4.2$ 
-sh-4.2$ pwd
**/home/ldap/ldapuser1 **
```












