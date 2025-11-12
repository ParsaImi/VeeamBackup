# VeeamBackup

## Introduction

This is a backup and restore solution for Esxi with VeeamBackup

### Backup Solution

- Connecting to Esxi Server

1- in the inventort tab, click on the Virtual Infrastructure

2- click on the Add Server

3- click on the VMware vSphere

4- click on the vSphere

5- add your Esxi server domain or ip address

6- add your Esxi username and password

- Create a backup job

1- click on the esxi server at the left side ( virtual infrastructure section )

2- Right click on the VM that you want to backup

3- click Add to Backup Job

4- click New Job

5- add a name for the job

6- select your VM

7- select the backup repository


### Restore Solution

1- using Veeam backuo & replication software

1- in Home tab of veeam backup, click on the restore section

2- click on the VMware vSphere

3- click on the Restore from backup

4- click on the Entire VM restore

5- Entire VM restore

6- click on the Add button add your backup vm

7- click on the Restore to a new location, or with different settings ( if you want to restore to a different directory )

8- click on your vm and host

9- click on the default resource pool

10- click on the default datastore

11- choose a name for the new vm

12- click on the default network

13- and Done!




2- restoring a vm without Veeam Backup & Replication software

- Using Veeam.Backup.Extractor.exe to convert the backup to a .vmdk file

1- chose the backup file

2- chose the target folder where the files will be extracted


- Send extracted files to the Esxi server datastore

You can do this in two ways

A- in esxi web console, go to the datastores section and click on datastore browser and upload the files

B- move backup files to an external hard drive and connect it to the esxi server. then :

1- setup a windows vm for accessing the hard drive

2- in windows VM page of esxi ui, click on the edit in top of the screen

3- click add other devices

4- first, add a usb controller

5- then, add a usb device ( the usbarbitrator should be on in the esxi server )

```
/etc/init.d/usbarbitrator start

chkconfig usbarbitrator on
```

6- boot the windows vm and install a tool like winscp to access the hard drive and esxi datastore

7- move all of the extracted files to the esxi datastore located at /vmfs/volumes/YOUR DATASTORE NAME

8- head back to the esxi web console and click on the datastore browser and you should see the files

9- right click on the file with .vmx extension and click on register vm

10- you should see the vm restored in Virtual Machines section 



