# ![EVOS Coin](https://evos.one/wp-content/themes/ivana_template_v7/images/logo.png)

Use this instructions to install the wallet,  and setup single masternode on Windows machine (HOT wallet/s).


## Table of Content
* [1. Desktop Wallet Preparation](#1-desktop-wallet-preparation-)
* [2. Masternode Setup](#2-masternode-setup-)
	* [2.1 Send the coins to your wallet](#21-send-the-coins-to-your-wallet)
	* [2.2 VPS setup](#22-vps-setup)
	* [2.3 Add masternode on the desktop wallet](#23-add-masternode-on-the-desktop-wallet)
	* [2.4 Automatic Masternode Setup](#24-automatic-masternode-setup)
	
* [3. FAQ](#3-faq)

## 1. Desktop Wallet Preparation

### 1.1 Setup the wallet
1. Download the [wallet](https://github.com/EVOS-DEV/evos-core/releases)
2. Start the wallet and wait for the sync. (30min to 10h depending on the number of the connections)
	
## 2. Masternode Setup

### 2.1 Send the coins to your wallet. Open Console (Tools => Debug console)
1. Create a new address. `getnewaddress MN1`
2. Send exactly 10000.00 coins to the generated address. (Send all coins in one transaction, fees should be paid additionally on top on 10K amount)
3. Wait for the at least 1 confirmation of the transaction.
4. Generate a new masternode private key by running the following command in wallet debug console `masternode genkey`.
5. Take txID of collateral transaction by running the following command in wallet debug console `masternode outputs`. 
6. Do not close console, or copy results to any place.

### 2.2 VPS setup
1. Register on: 
   - [Aruba] https://www.arubacloud.com/vps/virtual-private-server-range.aspx and setup small VPS server (for 1 eur/month) OR
   - [Vultr] https://www.vultr.com OR
   - [DigitalOcean] https://digitalocean.com (do not forget verify your e-mail)

2. Deposit some fund to your account to deploy a server. 
3. Recommended server configuration:  
   - OS: Ubuntu 16.04
   - Memory: 1GB (This server is capable to run 3 masternodes. One masternode need 150-300Mb memory)
   - Storage: 10GB minimum free space

### 2.3 Add masternode on the desktop wallet

1. Open your local wallet 
2. Open 'masternode.conf' file in text editor from the main/top menu (Tools->Open Masternode Configuration File)
3. Add new line and construct the new Masternode configuration by copying your masternode private key, transaction id and transaction index from step 2.1.4 and 2.1.5 (see below for example)
   
  *It should look like:* 
  MN1 [IP address]:16345 masternodeprivkey [10K desposit transaction id. 'masternode outputs'] [10K desposit transaction index. 'masternode outputs']
   
  *For example:* 
  `MN1 192.168.1.1:16345 92dnFYQMfsyMjPGbtWgcMgiAiMaZ75HX2EFohRxQVgJKLXFXTkQ 79b1a6e59d1bd0d9a9492ee25b61645a1985c6cca3dab8af4da85f24871db925 1`

   - Label: `MN1`
   - IP Address and port: `192.168.1.1:16345`
   - Private key: `92dnFYQMfsyMjPGbtWgcMgiAiMaZ75HX2EFohRxQVgJKLXFXTkQ`
   - Transaction ID: `79b1a6e59d1bd0d9a9492ee25b61645a1985c6cca3dab8af4da85f24871db925`
   - Output index:  `1`

  

4. Save file (masternode.conf)
5. Restart wallet.
6. You must wait 15 confirmations of collateral transaction (10000.00 EVOS)


### 2.4 Automatic Masternode Setup
1. Download [putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.70-installer.msi)
2. Start putty and login as root user. (Root password and server ip address are on your VPS management page)
3. Recommended to run following command before starting the installation script `apt-get update && apt-get upgrade`
4. To start the installation, paste this command and enter your private key during the process:
- For local wallets running on Windows use this command:
```
bash <( curl https://raw.githubusercontent.com/EVOS-DEV/MN-Setup/master/install.sh )

```
5.  Once script copmletes with wallet syncing follow go to tab Masternodes in your local wallet and press 'Start missing' button.


Congratulations!!
Your MN is now started!!   
	

## 3. FAQ


1. How can I get my masternode rewards transfered to other address?
   - Enable coin control feature in your wallet (Settings => Options => Display => Display coin control feature)
   - Go to send tab
   - Press the button `Open Coin Control`
   - Select from the input list button only the inputs with amounts different of MN collateral (10000.00)
   - Click OK
   - You can send selected amount to any valid EVOS address.
   - Note: DO NOT EVER Transfer EVOS from that original 10K deposit or you'll break your Masternode.

2. What is the password for the EVOS account on VPS?
   - There is no default password. When you create a user it does not have a password.

3. I get the following error: "Could not allocate vin".
   - Make sure your wallet fully synced and UNLOCKED.

4. How many masternodes can I run using one IP/server?
   - The limit is only the memory. One masternode requires 150-300MB RAM. A server with 1GB memory can run 3 masternodes. Each EVOS MN requires own public IP, so you will need additional IP address(es) to run multiple EVOS MNs on same server.

5. I got stuck. Can you help me?
   - Try to get help from the community and remember to get help only in public channels. Look for our moderators first!
     - [EVOS Discord](https://discord.gg/FeUc93R)
     - [https://bitcointalk.org/index.php?topic=5020175 ](https://bitcointalk.org/index.php?topic=5020175 )
