XMD POOL
====================

XMD COIN POOL

Get a fresh ubuntu 14.04 machine (you can get one from digital ocean for 5$ : https://m.do.co/c/6e83df0e17c6 or use any spare ubuntu machine)

Forward ports 63666 and 63667 and 3333 and 5555 and 7777 and 80 (if on azure)

Login

create a sudoer user with username : "azureuser" (If you are advanced linux user just change the "azureuser" references in all the files bellow, but i recommend you just create the "azureuser" user if you want this up in the next 5 minutes!)

Login as this user 

sudo -s

apt-get update

sudo apt-get install  redis-server  nodejs-dev nodejs-legacy npm nginx monit -y

curl -sL https://raw.githubusercontent.com/upggr/xmd-seed/master/install.sh | sudo bash -    (if this fails, just wget the file and execute it after chmod +x)

git clone https://github.com/upggr/xmd-pool.git pool     (or fork this repo, and make changes bellow so you can auto update with git when you need to)

./simplewallet                   (create a new wallet and record the wallet's address)

cp /home/azureuser/xmdcoin/xmadsimplewallet.conf /etc/init/xmadsimplewallet.conf

cp /home/azureuser/xmdcoin/startpool.conf /etc/init/startpool.conf

cp /home/azureuser/xmdcoin/checkpool /etc/monit/conf.d/checkpool

nano /home/azureuser/pool/config.json       (and edit the wallet address ("poolAddress") putting the above one in.)

nano /home/azureuser/pool/website/config.js (and change the references to the hostname of this server ("api" and "poolhost"))

cd pool

npm update

rm -rf /usr/share/nginx/html/

ln -s  /home/azureuser/pool/website /usr/share/nginx/html

start xmadsimplewallet

start startpool


visit your hostname or ip and see your pool running..  You can reboot your machine and make sure your pool still autostarts.

**want to reset your pool? just run redis-cli FLUSHALL (this will flush all users and rewards - caution)
