# Cold wallet Quantis masternode Guide for Windows Server  
The guide below is done using Windows Server 2012R2.  
Hot wallet is not recommended because of security risks.

##### Please use at your own risk!
### Overview  
1. Requirements  
2. Local Windows wallet setup1  
3. Windows VPS setup  
  3-1. Download wallet and config file setup  
  3-2. Firewall setup  
4. Local Windows wallet setup2  
5. Starting Masternode  
6. Checking masternode status  
7. How to manage the coins
8. Official links  
___
### 1. Requirements
* 5001 QUAN (5000 collateral + 1 to cover any TX fees)  
* Windows VPS server  
* A local home PC
___
### 2. Local Windows wallet setup1  
Download latest windows wallet from official release : [GitHub](https://github.com/QuantisNetwork/Quantis-public/releases)  
Open the wallet    
Go to `Receive` tab  
![walletsetup1](https://user-images.githubusercontent.com/38932966/42698634-74b35cde-86f9-11e8-99ed-ff033b1407eb.png)

Click `New Address` and enter label name(e.g. MN01) and click `OK`(do NOT check `Stealth Address`)  
![walletsetup2](https://user-images.githubusercontent.com/38932966/42698674-8f061f68-86f9-11e8-87fd-9825b35628f4.png)

Select the created address and click `Copy Address`  
![walletsetup3](https://user-images.githubusercontent.com/38932966/42698738-c1142914-86f9-11e8-904b-d6495ff2e8b5.png)

Go to `Send` tab
Paste on `Pay To` box and enter 5000 on `Amount` box  
*Nortice : Ensure that must be sent exactly 5000 QUAN and do it in a single transaction*  
![walletsetup4](https://user-images.githubusercontent.com/38932966/42699135-ca55aa6a-86fa-11e8-82c1-ad7c7954eada.png)

Use "Coin Control" feature when setting the second and the subsequent masternode and do NOT check the boxes of collaterals. (See the step 8)  

Click `Send`(do NOT check `Darksend`)  
Go to `Help` -> `Debug window`  
![walletsetup5](https://user-images.githubusercontent.com/38932966/42730729-c6860794-8836-11e8-996d-e672116672a1.png)

Open `Console`and type `masternode genkey`  
![walletsetup6](https://user-images.githubusercontent.com/38932966/42730757-8763d860-8837-11e8-848d-7d795eef3e77.png)

Write down the key(or leave the window as it is)  
Wait for 15 confirmations(Go to next step while waiting)   
___  
### 3. Windows VPS setup  
#### 3-1. Download wallet and config file setup
Run Windows update and restart the server
Download latest windows wallet from official release : [GitHub](https://github.com/QuantisNetwork/Quantis-public/releases)  
Open the wallet to make data files and folders (They are created automatically and you don't need to wait that the wallet is synced at this time)  
Close the wallet  
Press Windows key + R key  
Input "%appdata%" then press Enter key   
Open "Quantis" folder  
Open "quantis.conf" file  
Paste those settings and edit rpcuser, rpcpassword, masternodeprivkey, masternodeaddr  
Save and close the file  
___
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
masternodeprivkey=your private key(Generated in the step 2)  
masternodeaddr=your VPS IP:5050  
___
#### 3-2. Firewall setup  
Open `control panel` -> `System and Security` -> `Windows Firewall`  
Open `Advanced settings`  
![firewall](https://user-images.githubusercontent.com/38932966/42580081-aec70204-8564-11e8-92cd-a39bc6a54ace.png)


Click on `Inbound Rules` and `New Rule...`  
![firewall2](https://user-images.githubusercontent.com/38932966/42580212-00ac7e0a-8565-11e8-8b1c-4b4a12fc6d29.png)

Select `Port` then click on `Next`  
![firewall3](https://user-images.githubusercontent.com/38932966/42580310-2af2d8e4-8565-11e8-97e3-846d79dead13.png)

Select `TCP`, `Specific local ports`, input 5050 and then click on `Next`  
![firewall4](https://user-images.githubusercontent.com/38932966/42580326-35c7394a-8565-11e8-93f9-2d51aecf2b97.png)

Select `Allow the connection` then click on `Next`  
![firewall5](https://user-images.githubusercontent.com/38932966/42580340-3d6f2694-8565-11e8-80f4-69d49551e80f.png)

Click on `Next`  
![firewall6](https://user-images.githubusercontent.com/38932966/42580361-49e60d7a-8565-11e8-90a1-d709bcab2821.png)

Input "Quantis" in the name section then click on `Finish`  
![firewall7](https://user-images.githubusercontent.com/38932966/42580370-51544d7e-8565-11e8-8db0-5736902624d1.png)

Start the wallet on the VPS
___
### 4. Local Windows wallet setup2  
Back to the local wallet  
After 15 confirmations type `masternode outputs` on `Debug window`  
Press Windows key + R key  
Type `%appdata%/Quantis` and press enter key  
Edit `masternode.conf` as described below  
(If the file doesn't exist, make a new text file and rename to `masternode.conf`)     

`label vpsIP:port masternodekey collateraltx index`  
(e.g. MN01 123.456.789.0:5050 1234567890asdfghjk d0a362e103f7111489103bb99ea7f08b 0)  

(masternode key and collateraltx and index are pasted from `Debug window`)  
Save & close masternode.conf file  
Close the wallet and restart it   
___
### 5. Starting Masternode  
Check if both local and VPS wallet are fully synced  
Go to `Masternodes` tab    
Go to `My Master Nodes`  
Click on `Update`  
Select an alias you made in the step2  
Click on `Start`  
Approximately 30 seconds later your masternode will appear on `Quantis Network`
___
### 6. Check masternode status  
After about 30 minuites, your masternode `Active(secs)` will be reflected  
(It is recommended that you check your masternodes status with clicking `Update` regularly)

### Happy masternoding!
___
### 7. How to manage the coins  
You can use "Coin Control" function

Click on `Settings` and `Options...`  
![coincontrol1](https://user-images.githubusercontent.com/38932966/42692890-338e2d76-86e8-11e8-92ff-5bcba74af657.png)  

Go to `Display` tab and enable `Display coin control features (experts only!)` then click on `OK`  
![coincontrol2](https://user-images.githubusercontent.com/38932966/42692944-627868ea-86e8-11e8-9683-e28b8a0e9e67.png)

Go to `Send` tab and click on `Inputs...`  
![coincontrol3](https://user-images.githubusercontent.com/38932966/42695678-1ee08d48-86f1-11e8-886d-eb65c5508fe3.png)

It's default of `Coin Control`  
If you click on the triangle, the contents will be expanded  
![coincontrol4](https://user-images.githubusercontent.com/38932966/42695795-58370568-86f1-11e8-8a4f-8d2a34f61896.png)

It's useful for checking collateral  
![coincontrol4-2](https://user-images.githubusercontent.com/38932966/42697046-fb363b6e-86f4-11e8-8b0e-de2831616436.png)

You can select coins you want to send with checking the boxes
![coincontrol5](https://user-images.githubusercontent.com/38932966/42695858-7c409dca-86f1-11e8-80fc-2a995343ddce.png)

For example, When you add a master node or send some coins to other address click on `List mode`, `(un)select all` and UNCHECK all the boxes of collaterals then click on `OK`  
![coincontrol6](https://user-images.githubusercontent.com/38932966/42695876-89af5730-86f1-11e8-8421-7fc504953388.png)

<font color="crimson">Attention: If you forget uncheck the boxes of collaterals, your masternodes will be stopped. You need to resend collaterals to recover the masternodes.  </font>
### 8. Official links  
Bitcointalk: https://bitcointalk.org/index.php?topic=3354132.0  
Explorer: https://quantis.blockxplorer.info/  
Discord: https://discord.gg/EKsudbR  
Twitter: https://twitter.com/QuantisNetwork  
Facebook: https://www.facebook.com/Quantis-107598363410217/  
Website: http://quantis.network  

### Please help us raise funds!  

#### Official development funds  
Quantis wallet: QaeLt6Tt4YVNbS9zWTRSAe6D6jDbzhJD5x  
Bitcoin wallet: 14STYDo6HVKEcmtXYzut1ydbxJo3aSkX2b  
Ethereum wallet: 0x0fa44eB309811A3A24FC9095aEACb4d52B0b3238  

Thanks
