---
title: "Extension of Logical Volume in Linux"
seoTitle: "Mastering Linux Logical Volume Management: A Guide to Optimizing Disk"
seoDescription: "Learn the ins and outs of Linux Logical Volume Management (LVM) and discover how to efficiently manage and allocate disk space on your Linux systems."
datePublished: Mon Feb 13 2023 09:23:06 GMT+0000 (Coordinated Universal Time)
cuid: cle2lxxkn000d09mec9zz5k0t
slug: extension-of-logical-volume-in-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1676272616430/e8ba8dc7-686d-46ea-8f9c-5eab843fcb1b.png
tags: linux, projects, devops, technical-writing-1, lvm

---

# Concept :

* As PV (Physical Volume) and VG (Volume Group) are techniques used by LVM, Logical volume (LV) is also a technique used by LVM. LV is the main reason why we have the physical volume and volume group in place. The idea is to make storage management easier and more flexible as we mentioned earlier. Logical volumes with various sizes can be created on a volume group.
    

* As you can see in the above image, different PVs together made a Volume Group. The size of the VG will be the same as the addition of all the PVs.
    
    Suppose we have 3 PV of - 5 GB, 10 GB, and 15 GB; the Size of the VG will be (5+10+15) GB = 30 GB.
    
* In Linux, rather than counting and accepting the size of each PV, it considers the overall size of the VG and the VG acts as a 'storage pool' and then it let us create LV on top of it.
    

If you want to know more about LVM, let me know in the comment section! :)

Let's move on to today's topic :

# ***Extension of Logical Volume in Linux***

## Step-1:

Check the current status of PV, LV, VG and disk space.

*Make sure you are using "sudo".*

Run the commands,

**(a) lvs :** to check current LV status

**(b) vgs** : to check current VG status

**(c) pvs** : to check current PV status

**(d) df -hT** : to check disk space usage of the file system.

**(e) lsblk** : to list the storage devices along with their partitions.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676274853189/88a0afa5-ecb5-4d63-b509-c20e1541713b.png align="center")

## Step-2 :

To extend the LV, you need more space in VG(if there is not enough), and to add more space in VG, you need to add PV. And to add PV, again, you need to add a physical disk.

So, our first process will be to add a new disk. You can use various ways as per your environment. As I am using Oracle VM Virtual box, I will simply stop the server. go to storage and will add a new disk of, let's take, "5 GB" and will start the machine.

Now, after giving the "`lsblk`" command, you can see, a new physical disk called **"sdb"** of 5 GB, added to our machine.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676276243257/2532ad20-2926-4fe8-a039-dfba2cc5e4ec.png align="center")

## Step-3 :

Now we have to transform the "**physical disk**" to "**physical volume**".

(a) Run command `pvcreate /dev/<disk_name>`

(b) Now check current PVs, with `pvs` command and you will see a new "Physical **Volume**" added.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676276703063/c9caed3b-f6ff-4023-a7e4-52dd6260195f.png align="center")

## Step-4 :

Now as physical volume is present, we have to extend our existing VG to have more space. You can extend up to\* all the free space present in the new PV.

\*- As here we have added 5 GB, you can extend up to 5 GB in VG, you can do an extension of 1 GB, 2GB or 5 GB, as per your requirement.

Here, we will do it for the whole 5GB.

To extend the VG,

(a) Run command `vgextend <vg_name> /<pv_name>`

For me, it will be `vgextend ubuntu-vg /dev/sdb`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676277920703/bd784f01-20db-4199-9a20-d1ea1c3fc940.png align="center")

As you can see, after successfully extending VG, now free space increased from 11.50 gb to 16.50 gb.

## Step-5 :

As we have added space in VG, you can either create a new LV or extend the existing LV based on your requirement. As storage is added to the '**disk pool**' , you can play on your own :).

Here we will do both. :)

### (1) Extension of existing LV :-

To do this, we will run the command `lvextend -L +<size>G /dev/<vg_name>/<lv_name> -r`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676279069694/451d101b-dce1-41d9-8b94-05b2bd3160f0.png align="center")

As you can see in above screenshot, where, "***\-L" represents "length"*** and "***\-r " represents "resize"***, we have successfully extended the existing LV to 2 Gb.

### (2) Creating of New LV :-

To do this, we will run the command lvcreate -L +&lt;size&gt;G &lt;lv\_name&gt; &lt;vg\_name&gt;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676279458809/e83c7475-c6f9-40b6-856d-ea4635e001ce.png align="center")

As you can see , I have successfully created a new LV and assigned 2GB from the VG.

## Step-6 : The Conclusion:

Check the current status of all the items, you have checked in Step-1.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676279665879/af0a9dee-5e79-4b5e-a220-84776352c432.png align="center")

In conclusion, the Linux Logical Volume Manager (LVM) is a game-changer in the world of disk management. By using LVM, you have the flexibility to manage and allocate disk space in ways that were once impossible. Embrace the power of LVM and take your Linux systems to new heights of performance and efficiency.

Happy Learning :).