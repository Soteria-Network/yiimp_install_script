# Yiimp_install_script (update December, 2025)

Official Yiimp (used in this script for Yiimp Installation): https://github.com/Soteria-Network/yiimp

---

## Install script for yiimp on Ubuntu Server 22.04

USE THIS SCRIPT ON FRESH INSTALL UBUNTU Server 22.04 !

Connect on your VPS =>

- apt update
- apt upgrade
- reboot
- adduser pool (pool it's just an example...)
- adduser pool sudo
- su - pool
- exit
- su - pool
- sudo apt -y install git
- git clone https://github.com/Soteria-Network/yiimp_install_script.git
- cd yiimp_install_script/
- sudo apt install php8.2-fpm php8.2-cli php8.2-mysql php8.2-curl php8.2-gd php8.2-xml php8.2-mbstring unzip
- bash install.sh (DO NOT RUN THE SCRIPT AS ROOT or SUDO)
  To check your server’s public IP quickly, run:
- curl ifconfig.me or wget -qO- ifconfig.me // This will return the correct public IP to enter into the installer.
- Enter the Public IP of the system you will use to access the admin panel (IP of YOUR PC where need to be access to Panel) : If you want to restrict admin panel access to only your own PC, you should enter your PC’s public IP address (the one your ISP assigns). You can find it by visiting https://ifconfig.me or https://whatismyipaddress.com from your PC.

If your IP changes frequently (dynamic IP), you may get locked out later. In that case, you can either:

    Enter 0.0.0.0 or leave it blank to allow access from any IP (less secure).

    Or use a static IP / VPN with a fixed exit IP so you always connect from the same address.

If you’re just testing locally and don’t care about restrictions, you can put the server’s own public IP (e.g., 37.224.20.228) so you can reach the panel from anywhere.
- At the end, you MUST REBOOT to finalize installation...

Enable and start php‑fpm
sudo systemctl enable php8.2-fpm
sudo systemctl start php8.2-fpm
sudo systemctl status php8.2-fpm

Check web services
- sudo systemctl status nginx
- sudo systemctl status php8.2-fpm
Finish !

- Go http://37.224.20.228 or https://37.224.20.228 (if you have chosen LetsEncrypt SSL). Enjoy !
- Go http://37.224.20.228/site/myadmin or https://37.224.20.228/site/myadmin to access Panel Admin

If you are issue after installation (nginx,mariadb... not found), use this script : bash install-debug.sh (watch the log during installation)

###### :bangbang: **YOU MUST UPDATE THE FOLLOWING FILES :**

- **/var/web/serverconfig.php :** update this file to include your public ip (line = YAAMP_ADMIN_IP) to access the admin panel (Put your PERSONNAL IP, NOT IP of your VPS). update with public keys from exchanges. update with other information specific to your server..
- **/etc/yiimp/keys.php :** update with secrect keys from the exchanges (not mandatory)
- **If you want change 'AdminPanel' to access Panel Admin :** Edit this file "/var/web/yaamp/modules/site/SiteController.php" and Line 11 => change 'AdminPanel'

###### :bangbang: **IMPORTANT** :

- The configuration of yiimp and coin require a minimum of knowledge in linux & many beers...
- Your mysql information (login/Password) is saved in **~/.my.cnf**

---

###### This script has an interactive beginning and will ask for the following information :

- Server Name (no http:// or www !!!!! Example : crypto.com OR pool.crypto.com OR 80.41.52.63)
- Are you using a subdomain (mypoolx11.crypto.com)
- Enter support email
- Set stratum to AutoExchange
- Your Public IP for admin access (Put your PERSONNAL IP, NOT IP of your VPS)
- Install Fail2ban
- Install UFW and configure ports
- Install LetsEncrypt SSL

---

**This install script will get you 95% ready to go with yiimp. There are a few things you need to do after the main install is finished.**

While I did add some server security to the script, it is every server owners responsibility to fully secure their own servers. After the installation you will still need to customize your serverconfig.php file to your liking, add your API keys, and build/add your coins to the control panel.

There will be several wallets already in yiimp. These have nothing to do with the installation script and are from the database import from the yiimp github.
