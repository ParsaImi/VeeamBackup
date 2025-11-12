# Veeam Backup

## Introduction

This is a backup and restore solution for ESXi using Veeam Backup.

## Backup Solution

### Connecting to ESXi Server

1. In the Inventory tab, click on **Virtual Infrastructure**
2. Click on **Add Server**
3. Click on **VMware vSphere**
4. Click on **vSphere**
5. Add your ESXi server domain or IP address
6. Add your ESXi username and password

### Creating a Backup Job

1. Click on the ESXi server on the left side (Virtual Infrastructure section)
2. Right-click on the VM that you want to backup
3. Click **Add to Backup Job**
4. Click **New Job**
5. Add a name for the job
6. Select your VM
7. Select the backup repository

## Restore Solution

### Method 1: Using Veeam Backup & Replication Software

1. In the Home tab of Veeam Backup, click on the **Restore** section
2. Click on **VMware vSphere**
3. Click on **Restore from backup**
4. Click on **Entire VM restore**
5. Click on the **Add** button to add your backup VM
6. Click on **Restore to a new location, or with different settings** (if you want to restore to a different directory)
7. Click on your VM and host
8. Click on the default resource pool
9. Click on the default datastore
10. Choose a name for the new VM
11. Click on the default network
12. Done!

### Method 2: Restoring a VM Without Veeam Backup & Replication Software

#### Using Veeam.Backup.Extractor.exe to Convert the Backup to a .vmdk File

1. Choose the backup file
2. Choose the target folder where the files will be extracted

#### Sending Extracted Files to the ESXi Server Datastore

You can do this in two ways:

**Option A: Via ESXi Web Console**

1. In the ESXi web console, go to the **Datastores** section
2. Click on **Datastore Browser**
3. Upload the files

**Option B: Via External Hard Drive**

1. Move backup files to an external hard drive and connect it to the ESXi server
2. Set up a Windows VM for accessing the hard drive
3. In the Windows VM page of the ESXi UI, click on **Edit** at the top of the screen
4. Click **Add Other Devices**
5. First, add a USB controller
6. Then, add a USB device (the usbarbitrator should be enabled on the ESXi server)

   ```bash
   /etc/init.d/usbarbitrator start
   chkconfig usbarbitrator on
   ```

7. Boot the Windows VM and install a tool like WinSCP to access the hard drive and ESXi datastore
8. Move all of the extracted files to the ESXi datastore located at `/vmfs/volumes/YOUR_DATASTORE_NAME`
9. Head back to the ESXi web console and click on the **Datastore Browser** and you should see the files
10. Right-click on the file with `.vmx` extension and click **Register VM**
11. You should see the restored VM in the **Virtual Machines** section
