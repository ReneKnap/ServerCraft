# HBA SAS cards
It is recommended to check whether your target HBA card will support the fill bandwidth of your connected SAS / SATA devices. Cheap cards on Amazon or eBay tend to have too little PCIe bandwidth for the number rod SATA ports they have. 
Thus, it is more likely to get good hardware when searching for used server hardware like LSI HBA cards.
The following two cards are one of the most found cards on ebay and will work just fine. With a PCIe 2.0 8x interface they have up to 40Gb/s bandwidth for their 8 SAS / SATA ports which will theoretically support 48Gb/s. However if HDDs are used this theoretical bandwidth will not be needed. 
<font color="#ffff00">Information</font>: If the HBA card you want to use has a hardware RAID functionality build in and if you want to use it together with for instance unRAID or TrueNAS this hardware RAID functionality has to be disabled. Those NAS Operating Systems will use software RAID. The additional layer in form of hardware RAID between the OS and the drives themselves will make the setup unusable. Hardware RAID can be disabled by flashing custom BIOS to the HBA card. If the card is from LSI they can most of the time already be bought pre flashed with *IT mode* activated.

- LSI 9220-8i / ServeRAID M1015: ![[ibm_doc_sraidmr_m1015-2ndedition_user-guide.pdf]] (https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://download.lenovo.com/servers/mig/systems/support/system_x_pdf/ibm_doc_sraidmr_m1015-2ndedition_user-guide.pdf&ved=2ahUKEwio342IoIaAAxWbQ6QEHau_DBw4ChAWegQIFhAB&usg=AOvVaw3Sd_i-vYas8lmntDOlHnSs)
 
 - LSI 9211-8i: ![[LSISAS9211-8i_UG_v1-1.pdf]](https://www.broadcom.com/support/knowledgebase/1211161498134/lsi-sas-hba-os-support-list)
 
A general overview over the LSI hardware can be found here: (https://www.broadcom.com/support/knowledgebase/1211161498134/lsi-sas-hba-os-support-list)