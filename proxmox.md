# enable IOMMU if not available automatically
To enable IOMMU - which is an essential virtualization feature for the passthrough of PCIe devices - it can be necessary to edit the grub file of proxmox to enable this feature during startup.
Frist of all the CPU and the motherboard used have to support virtualization (e.g. VTd / VTx for Intel CPUS) and IOMMU. This has to be enabled in the BIOS since it is by mostly deactivated by default.
If proxmox can not find the IOMMU feature the grub file has to be edited. To check if IOMMU is available following command can be used:
`dmesg | grep -e DMAR -e IOMMU`
It should output something like this:
`[    0.028730] DMAR: IOMMU enabled`

If this is not the case the grub file located at `/etc/default/grub` has to be edited.
The file should bec edited to include the following line if an Intel CPU is used:
`GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on"`
After this change the system has to be updated using `update-grub` and rebooted.
Now grub should be available if it is supported by the system.<

# add pam user
First install sudo on proxmox if not already done:
`apt install sudo`
Then add the new user you want to add:
`adduser <username>`
Now you can add the user to the users table in your proxmox GUI, too. Then assign the permissions your new user shall have.