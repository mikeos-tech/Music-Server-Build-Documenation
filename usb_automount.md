# Auto Mounting USB Drives for Music Backups

*Ubuntu* Server does not automatically mount USB drives when they are connected, to enable this functionality you need to install the **usbmount** package (which the *install_software.sh* script file does.  Adding a line to the *fstab* file to set the location for the mount.

This command installs the **usbmount** package:

      sudo apt install -y usbmount 

An example line from an *fstab* file:

      /dev/sdc1␣/backup/␣␣auto␣nosuid,nodev,nofail,x-gvfs-show␣0␣0¬

This line in the *fstab* file will automatically mount any device attached as sdc1 in the */backup/* folder.


