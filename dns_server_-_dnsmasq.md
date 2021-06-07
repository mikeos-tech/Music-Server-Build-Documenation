# Installing and Configuring the dnsmasq Server

dnsmasq (DNS masquerade) is Open Source software that provides Domain Name System (DNS) caching, a Dynamic Host Configuration Protocol (DHCP) server, router advertisement and network boot features, intended for small computer networks.

I wanted to install a *DNS* server to provide easy, named access to the web pages and the files shares.  The *Samba* configuration also works to facilitate this. 

I left my Router providing the *DHCP* for my network.

I made the *DNS* available on my network by setting it up as the primary *DNS* server within my routers **LAN** settings, I had the option of setting two others which I set as the two *OpenDNS* servers.

You first need to disable *Systemd-resolved* service in your system. *Systemd-resolved* service is used for network name resolution to local applications.

      systemctl disable --now systemd-resolved

Once the service is disabled, you need to remove its default configuration file.  It should be removed rather than edited as it can be a link to another file. Removing it will break that link. 

      rm -rf /etc/resolv.conf

create a new *resolve.conf* file with the ip address of an external DNS server.

      nameserver 208.67.220.220

I chose to use one of the *OpenDNS* servers, I have included a list of available *DNS* servers below:

* 1.1.1.1 - Cloudflare
* 1.0.0.1 - Cloudflare
* 4.2.2.1 - Layer 3
* 4.2.2.2 - Layer 3
* 4.2.2.3 - Layer 3
* 8.8.8.8 - Google
* 8.8.4.4 - Google
* 208.67.222.222 - OpenDNS
* 208.67.220.220 - OpenDNS

## Install the **dnsmasq** sofware

      sudo apt install dnsmasq dnsutils ldnsutils -y

It should be automatically started, check its status

      systemctl status dnsmasq

## Configure **dnsmasq**

Edit the /etc/dnsmasq.conf file:

      sudo vim /etc/dnsmasq.conf

The file is long, but go through the file and uncomment the lines I have listed below:

* port=53¬
* domain-needed¬
* bogus-priv¬
* listen-address=127.0.0.1,192.168.2.9¬
* expand-hosts¬
* domain=musicwoorld.com¬
* cache-size=1000¬

The last IP address on the **listen-address** after the , should be the address of the *DNS* server it's self.

The value for the **domain** should be the domain name you are using.  This is something that will only be used on your network.  It also need to be included the *host* file and I also included it within my router and my *FreeNAS* configuration.

I tried adding these lines at the start/end of the file and got errors so it's better to uncomment them.


## Update resolve.conf

The file: /etc/resolv.conf needs to be edited.

      sudo vim  /etc/resolv.conf

Update it to include the address of the server it's self, followed by an alternative Internet *DNS* server:

      nameserver 192.168.2.9
      nameserver 208.67.220.220

## Test the configuration

Run the command:

      dnsmasq --test

If all is well it should respond:

      dnsmasq: syntax check OK.

Restart *dnsmasq*

      systemctl restart dnsmasq

## Add it to the hosts file

Edit the /etc/hosts

     sudo vim /etc/hosts

Add a line to it pointing to your DNS server, below is what I added to mine.

      192.168.2.9␣musicmachine.musicwoorld.com

## Test the *DNS*

Test it with it's own name (this example uses the name I've used):

      dig musicmachine.musicwoorld.com +short

Which should return the servers IP address.

      dig google.com +short

Which should return an external IP address.

Add the following files to your configuration backup:

* /etc/dnsmasq.conf
* /etc/hosts
* /etc/resolv.conf
