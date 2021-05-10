#Transmission Configuration

##Things to include reminders
*  I have a folder mounted on my main machine which is a subfolder within my */Downloads/* folder, this allows me to easily save torrent files in the folder and have them automatically started/downloaded.
*    Where the folder is to map
*    the line from fstab
*  What did I change in the configuration file.
*  Transmission is loaded as a new tab

In the *installation script* - get actual name these two lines are included, this adds the *ppa* to a Ubuntu distribution so the application can be installed and updated.
    sudo add-apt-repository ppa:transmissionbt/ppa
    sudo apt install transmission



This command enables the *debian-transmission* group, which is the owner of the files to read the file.  If the standard user is a member of the group it will allow them to copy/backup the file in scripts run in their user name.
    sudo chmod g+r /etc/transmission-daemon/settings.json
