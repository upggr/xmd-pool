XMD POOL
====================

XMD COIN POOL

Get a fresh ubuntu 14.04 machine

Forward ports 63666 and 63667 and 3333 and 5555 and 7777 and 80 (if on azure)

Login

creade a suer user with username : "azureuser" (or change "asureuser" to your user in all the things bellow an the setup scripts from github... - Just create auser names azureuser, lot simpler and will work 100%)
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
