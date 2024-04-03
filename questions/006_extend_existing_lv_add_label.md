# Extend existing logical volume by 200MB and add label to it 

## Question
Extend the existing file system to a total size of 200MB and add a label called myFS.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

## Answer
Before any kind of operations on LVM it is good to know what we actually have in the system. The proper command to list all devices we can use is in order `pvs`, `vgs` and `lvs`. It shows all physical storages and devices, volume groups and logical volumes.

### xfs
Exam objectives require extending of logical partitions. The tricky part here is to remember that xfs filesystem (which is the default setting for RHEL) does not allow downsizing of xfs partition (the only possibility is to grow that volume). So please be careful when reading LVM related questions during the exam.
  
When the question is presented in this form, we can assume that the logical volume is less than the given 200MB we have to set. Then we can use: 
```
# notice -r flag which indicates not only to resize logical volume but also filesystem on it
lvextend -r –L 200M /dev/VOLUME_GROUP/LOGICAL_VOLUME

# Alternatively
lvextend –L 200M /dev/VOLUME_GROUP/LOGICAL_VOLUME
xfs_growfs /dev/VOLUME_GROUP/LOGICAL_VOLUME
```

In order to give a logical volume a label we have to unmount it first, set a label and then mount it again:
```
# umount /LINK/TO/FILESYSTEM/MOUNT/POINT
# xfs_admin -L "myFS" /dev/VOLUME_GROUP/LOGICAL_VOLUME
# mount /LINK/TO/FILESYSTEM/MOUNT/POINT
```

## Aditional comments
According to the fs type, the tool for growing or reducing it changes
| FS Type | Tool |
|---------|------|
| xfs | `xfs_growfs` or `fsadm resize` |
| ext | `resize2fs` or `fsadm -e resize` |
| vfat/fat32/ntfs/msdos | N/A |
