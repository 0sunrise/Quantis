# Quantis Masternode Setup Guide

The guide below is done using Ubuntu 16.04 64-bit.
### Overview
1. Requirements  
2. Local Windows wallet setup1
3. VPS setup  
    3-1. Install the dependancies(If already running other masternodes, skippable)  
      3.2. Open Firewall for Quantis  
    3-3. Compiling  
      3-3-1. Setup swapfile  
      3-3-2. Downloading Quantis source code from official release  
      3-3-3. Compiling  
    3-4. Setup conf file  
    3-5. Starting wallet daemon
4. Local Windows wallet setup2  
5. Starting Masternode  
6. Checking masternode status  
7. Official links
<!--3-3. Download the wallet and extract from the archive-->  
___
### 1. Requirements
* 5001 QUAN (5000 collateral + 1 to cover any TX fees)  
* VPS server (Recommended VPS size at least 1GB RAM)
___
### 2. Local Windows wallet setup1  
Download latest windows wallet from official release : [GitHub](https://github.com/QuantisNetwork/Quantis-public/releases/download/Publicrelease)  
Open the wallet    
Go to `Receive` tab  
Click `New Address` and enter label name(ex. masternode-1) and click `OK`(do NOT check `Stealth Address`)  
Select the created address and click `Copy Address`  
Go to `Send` tab
Paste on `Pay To` box and enter 5000 on `Amount` box  
*Nortice : Ensure that must be sent exactly 5000 QUAN and do it in a single transaction*  
Click `Send`(do NOT check `Darksend`and `InstantX`)  
Go to `Help` -> `Debug window`  
Open `Console`and type `masternode genkey`  
Write down the key(or leave the window as it is)  
Wait for 16 confirmations(Go to next step while waiting)   
___
### 3. VPS setup  
Login to your VPS
#### 3-1. Install the dependancies
sudo apt-get update && apt-get upgrade  
sudo apt-get dist-upgrade  
sudo apt-get install libzmq3-dev libminiupnpc-dev libssl-dev libevent-dev -y  
sudo apt-get install build-essential libtool autotools-dev automake pkg-config -y  
sudo apt-get install libssl-dev libevent-dev bsdmainutils   software-properties-common
-y  
sudo apt-get install libboost-all-dev -y  
sudo add-apt-repository ppa:bitcoin/bitcoin  
sudo apt-get update  
sudo apt-get install libdb4.8-dev libdb4.8++-dev  -y  
sudo apt-get install libgmp3-dev  
#### 3-2. Open Firewall for the Quantis  
sudo ufw allow 5050/tcp  
##### System restart  
sudo reboot (If already active, sudo ufw reload)
#### 3-3. Compiling
##### 3-3-1. Setup swapfile  
fallocate -l 4G /swapfile  
chown root:root /swapfile  
chmod 0600 /swapfile  
sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"  
mkswap /swapfile  
swapon /swapfile  
Initialize swapfile automatically on boot  
echo '/swapfile none swap sw 0 0' >> /etc/fstab  
##### System restart  
sudo reboot
##### 3-3-2. Download Quantis source code from official release  
git clone https://github.com/QuantisNetwork/Quantis-public  
mkdir quantis  
##### 3-3-3. Compiling  
cd Quantis-public/src/leveldb  
chmod +x build_detect_platform  
make clean  
make libleveldb.a libmemenv.a  
cd ../  
make -f makefile.unix
mv quantisd ~/quantis/  
cd ~/
rm -r Quantis-public  

#### 3-4. Setup conf file  
cd ~/
mkdir .quantis  
nano ~/.quantis/quantis.conf  

Copy and paste those settings and change rpcuser,rpcpassword,masternodeprivkey,masternodeaddr

rpcuser=username(Configure your own)  
rpcpassword=password(Configure your own)  
rpcallowip=127.0.0.1  
rpcport=5051  
daemon=1  
server=1  
listen=1  
logtimestamps=1  
maxconnections=256  
masternode=1  
masternodeprivkey=your private key(Generated at step2)  
masternodeaddr=your VPS IP:5050  



Press Ctrl + x  
Press y  
Press enter  
#### 3-5. Start wallet daemon  
cd quantis  
./quantisd -daemon  
##### Usage  
Stop daemon  
./quantisd stop  

Display information  
[watch] ./quantisd getinfo  
[watch] ./quantisd getmininginfo  
[watch] ./quantisd getblockcount  
[watch] ./quantisd masternode status  

___
### 4. Local Windows wallet setup2  
Back to windows wallet  
After 16 confirmations type `masternode outputs` on `Debug window`
Press Windows key + R  
Type `%appdata%/Quantis` and press enter key  
Edit `masternode.conf`  
(If not exist make a new text file and rename to `masternode.conf`)     
`label vpsIP:port masternodekey collateraltx index`  
ex. Masternode-1 123.456.789.0:5050 1234567890asdfghjk 0  
(masternodekey and collateraltx and index are pasted from `Debug window`)  
Close `masternode.conf` and windows wallet  
___
### 5. Start Masternode  
Start windows wallet  
Go to `Masternodes` tab  
Wait until appear masternode list on `Quantis Network`  
Go to `My Master Nodes`  
Click `Update`  
Select Alias made at step2  
Click `Start`  
After a muinite your masternode will appear on `Quantis Network`
___
### 6. Check masternode status  
After 30 nuinites `Active(secs)` reflected on Your masternode  
It is Recommended to be checked by click `Update` regularly  

Happy masternoding!
___
### 7. Official links  
Bitcointalk: https://bitcointalk.org/index.php?topic=3354132.0  
Discord: https://discord.gg/EKsudbR  
Twitter: https://twitter.com/QuantisNetwork  
Facebook: https://www.facebook.com/Quantis-107598363410217/  
Website: http://quantis.network  

Please help us raise funds!  
Bitcoin wallet: 14STYDo6HVKEcmtXYzut1ydbxJo3aSkX2b  
Ethereum wallet: 0x0fa44eB309811A3A24FC9095aEACb4d52B0b3238  

Thanks
