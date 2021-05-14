Install Webmin
Webmin provides a graphical user interface that enables you to carry out administration tasks remotely.

As far as the media server is concerned this will be to trigger updates and to shutdown and restart the server.

The alternative would be to SSH into the server and carry out these tasks from the command line.

Webmin provides a lot of additional functionality that may be useful if you are using the server for any additional functionality.

https://www.digitalocean.com/community/tutorials/how-to-install-webmin-on-ubuntu-20-04


    sudo apt update
    sudo vim /etc/apt/sources.list

Add the line below to the bottom

    deb http://download.webmin.com/download/repository sarge contrib

    wget -q -O- http://www.webmin.com/jcameron-key.asc | sudo apt-key add
    sudo apt update
    sudo apt install webmin
    sudo ufw allow 10000
