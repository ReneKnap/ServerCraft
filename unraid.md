# Documentation
Documentation of unraid: https://docs.unraid.net/

# Storage Management
Documentation for storage anagement: [https://docs.unraid.net/unraid-os/manual/storage-management/](https://docs.unraid.net/unraid-os/manual/storage-management/ "smartCard-inline")

# NFS and SMB shares
It is recommended to use NFS shares as network storage for images of virtual machines or containers. This is because NFS supports virtual links, SMB does not. This can lead to problems with mounting VM or container images when using SMB shares to host them.
Especially in proxmox hosting images in an SMB share will not work.

A NFS share has to user / password authentication. You rather have to set a connection rule on the NFS server. This rule will allow a specified IP address to write to the share. Reading is however allowed to anyone in the network. The rule looks like this:
```
192.168.50.40(sec=sys,rw)
```