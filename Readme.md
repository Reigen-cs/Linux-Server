# Linux Server


## Creates VM


### 1) One VM to be a client workstation.

- Classic Ubuntu (dont forget on the first page of VirtualBox to mark the case "skip unattended installation" otherwise the terminal can crash)
- Don't forget to select **separate the /home partition** at the disk selection step.
- I set the following credentials
	- Username : client
	- Password : client

> Safety first you know !

### 2) One Debian server

- I set the following credentials
	- Username : root
	- Password : toor

> Again safety first !

### 3) Virtualbox

- Create a NAT network
	- go to `Tools` -> `Network` -> `Nat networks` 
	- set a name for the network, here i set **project**
	- then set a IPv4 range, here **10.0.2.0/24**
	- Don't check the `Enable DHCP` because we gonna put a static IP and a DHCP on the server that gonna give an ip to te client
- On both VM select `network` and set `nat network` and `project`

## Setup CLIENT device

First of all update the device
- `sudo apt update`
- `sudo apt upgrade`
- `sudo reboot`

### 1) Basic software installation 

- **LibreOffice:**  `sudo apt install libreoffice`
- **Gimp:** `sudo apt install gimp`
- **Web-Browser (Mullvad) :** `wget https://mullvad.net/fr/download/browser/linux64/latest` then `tar xf latest`. To launch the browser go into the folder and `./start-mullvad-browser.desktop

### 2) Remote acces

2 options SSH and a remote desktop solution:

**2.1 SSH**
- install openssh `sudo apt install openssh-server openssh-client`
- enable ssh `sudo systemctl enable ssh`

**2.2 Remote desktop**
- Select and install a software here i use _remmina_ `sudo apt install remmina`
- open the software and create a new profile
- Install the software to an other machine to connect to the client.


## Setup SERVER device

First of all as root update the device and install sudo package
- `apt install sudo`
- `apt update`
- `apt upgrade`
- `sudo reboot`

### 1) Create a new user for administration 

-  `adduser userName` here i put 

> Off course i like security so the password is tristan.

- now need to elevate the permission of this user to sudo `sudo usermod -aG sudo 

### 2) Setup a static IP

- First save the configuation to a file named config1 `sudo cp /etc/network/interfaces /etc/network/config1`
- then modify the interfaces `sudo nano /etc/network/interfaces`
	- comment this part `iface enp0s3 inet dhcp`
	- add :
		- `iface enp0s3 inet static`
		- `address 10.0.2.10`
		- `netmask 255.255.255.0`
		- `gateway 10.0.2.1`



- restart the network service `sudo systemctl restart networking.service`
- check if you have the good ip with a `ip a`
- you can also check if internet is available with a `ping google.com`


### 3) Install a firewall

Using ufw

- `sudo apt install ufw`
- Default parameter setting
	- `sudo ufw default deny incoming`
	- `sudo ufw default allow outgoing`
- Allow ssh connection `sudo ufw allow ssh` do the same and replace ssh by **http port** `80`, **https port** `443` and **DNS port `53` 
- Activate the firewall `sudo ufw enable`
- Can check status `sudo ufw status`

### 4) Check SSH 

- Go on client device and try ssh connection with the user admint. `ssh tX@10.0.2.10` should work.
- Then verify that root connection by ssh is not allowed. Make same command but with root user to verify.



### 5) GLPI, PHP, MariaDB and Apache

Do it as ROOT user :

- Easy script available on github just do `wget https://raw.githubusercontent.com/jr0w3/GLPI_install_script/main/glpi-install.sh && bash glpi-install.sh`
- Follow instructions and take note off the credentials.
)

- Normaly now  with your client device you can go to a web browser and indicate the ip of the server and manage GLPI
- **The script put basic credentials and password, can stay like that for the exercices, but in real life don't forget to change it**


### 6) DNS

I use this tutorial [Getting Started with the BIND DNS Server (adamtheautomator.com)](https://adamtheautomator.com/bind-dns-server/)
see here my setup


### 7) DHCP

**IS WORKING MTFK**

- Install ISC DHCP SERVER `sudo apt install isc-dhcp-server`
- Say wich interface gonna be used. Modify `sudo nano /etc/default/isc-dhcp-server`
	>`INTERFACESv4="enp0s3"` i put enp0s3 bc that's the interface i use

- configure the DHCP by modify the file `sudo nano /etc/dhcp/dhcpd.conf`
	- set the subnet, subnet mqsk, router and range like this.

	
- restart the service and the client device

### BACKUP

- first need to add a back up drive on the vm :
	- In VirtualBox, select the device and go to Settings.
	- Click on storage.
	- Click on the hard drive on "Controller:SATA".
	- Click Create
	- Leave VDI selected 
	- Allocate space
	- Select your new volume and click on "Choose".
	- turn on the VM and make a `lsblk` to verify if the newfrive is here

-  Now format the new drive `sudo mkfs.ext4 /dev/sdb`
-  create a backup folder `sudo mkdir /mnt/conf_backups`
- Make a script to save files on the backup drive:
	- Perform this as ROOT `su`
	- create the folder and file for the script : `mkdir scripts` then `nano /root/scripts/conf_backup.sh`
	- put this script in it :
> `sudo mount /dev/sdb /mnt/conf_backups/` -> Mounts a disk device (`/dev/sdb`) to the `/mnt/conf_backups/` directory
> 
  > `sudo mkdir /tmp/$(date +%d-%b-%Y)` -> Creates a temporary directory with a name based on the current date:
   >
   >`sudo cp -r /etc/bind /etc/dhcp /etc/apache2 /etc/mysql /etc/php /etc/resolv.conf /tmp/$(date +%d-%b-%Y)/` -> Copies the following directories and files to the temporary directory
   >
   >`sudo tar -zcvf /mnt/conf_backups/$(date +%d-%b-%Y).tar.gz /tmp/$(date +%d-%b-%Y)/` -> Creates a compressed tarball archive of the temporary directory:
   >
   >`sudo rm -rf /tmp/$(date +%d-%b-%Y)` -> Removes the temporary directory and its contents:
   >
   >`sudo umount /dev/sdb` -> Unmounts the disk device (`/dev/sdb`)
   
 - and finaly make a crontab to execute it at a specific time `sudo crontab -u root -e`
 - to make the save every saturday at 06h00 write this `00 06 * * 6 /root/scripts/conf_backup.sh`
>- `00`: Specifies the minute when the task should run (in this case, 0 minutes).
>- `06`: Specifies the hour when the task should run (in this case, 6 AM in 24-hour format).
>- `*`: Specifies any value for the day of the month field, meaning the task can run on any day of the month.
>- `*`: Specifies any value for the month field, meaning the task can run in any month.
>- `6`: Specifies the day of the week when the task should run (in this case, Saturday, where Saturday is represented by 6).
>- `/root/scripts/conf_backup.sh`: Specifies the command or script that should be executed at the specified time.
   
 
