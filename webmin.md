Install Webmin

https://www.digitalocean.com/community/tutorials/how-to-install-webmin-on-ubuntu-20-04


    sudo apt update
    sudo vim /etc/apt/sources.list

Add the line below to the bottom

    deb http://download.webmin.com/download/repository sarge contrib

    wget -q -O- http://www.webmin.com/jcameron-key.asc | sudo apt-key add
    sudo apt update
    sudo apt install webmin
    sudo ufw allow 10000
