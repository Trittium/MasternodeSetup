![Example-Logo](https://avatars.githubusercontent.com/u/74295691?s=460&u=d19fb6a5f6df729cb0d9f5478a1619edd56cd415&v=4)

# Trittium Masternode Setup Guide
***
## Required
1) **100000 TRTT coins**
2) **Local Wallet https://github.com/Trittium/trittium/releases**
3) **VPS with UBUNTU 16.04 or 18.04**
4) **Putty https://www.putty.org/**
5) **Text editor on your local pc to save data for copy/paste**
***

***On your Local Wallet***
* Create an address with a label MN1 and send exactly 100000 TRTT to it. Wait to complete 6 confirmations on “ Payment to yourself “ created.

* Open the Debug Console ( Settings –> Debug -> Console ) and type ***createmasternodekey***.
You will then receive your private key, save it in a txt to use it later.
  ```
  Example:
          createmasternodekey
          w8723KqiiqtiLH6y2ktjfwzuSrNucGAbagpmTmCn1KnNEeQTJKf
* Still at Debug Console type ***getmasternodeoutputs*** and save txhash and outputidx on a txt
  ```
  Exemple:
          "txhash" : "12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa",
		         "outputidx" : 0

***On Putty***

* Once logged in your vps, *copy/paste* each line one by one with *Enter*

	:arrow_forward: `wget -q https://github.com/Trittium/MasternodeSetup/raw/master/install.sh`

	:arrow_forward: `bash install.sh`


* Let this run, and when it ask you to install dependencies, if you're not sure press ***y*** and then enter

* It will take some time and then will ask to compile the Daemon, press ***y*** and then enter 

* Last thing script will ask you is to provide Masternode Genkey. Copy the one you got previously (createmasternodekey) and press enter.

Remember to do `trittium-cli getblockcount` to check if VPS catching blocks till it synced with chain, if not follow this procedure:

* Go to your wallet-qt and check peers list (click Peers button in row of buttons in top right corner of wallet, it is the one that looks like a radar or a wifi connnection icon) and select one ip from the list. With that ip do the follow command at VPS `trittium-cli addnode "ip" onetry`

      Example:
		  trittium-cli addnode 45.32.144.158 onetry
    
* Check now if VPS already downloading blocks with the command `trittium-cli getblockcount`, and if still downloading blocks then give it time now to catch last block number 

Do not close your terminal/ command prompt window at this point.

***Go back to your Local Wallet***

* Open the Masternode Configuration file (hover over each button in the row of buttons in top right of wallet and click the button that shows 'masternode.conf'). Add a new line to this file (without #) using the template below (bold words needs to be changed) then save and close the file.

**MNALIAS VPS_IP**:31001 **masternodeprivkey TXhash Output**

		Example:
		MN1 125.67.32.10:31001 w8723KqiiqtiLH6y2ktjfwzuSrNucGAbagpmTmCn1KnNEeQTJKf 12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa 0

* Close and Re-open Local Wallet, and at Masternode Tab you will find your MN with status MISSING

***(For the next steps you need to have already 16 confirmation on “Payment to yourself “ created in first step)***

* Go to Debug Console type the following: ***startmasternode alias 0 [MNALIAS]***

		Example:
		startmasternode alias 0 MN1
***

***Go back to Putty***

   :arrow_forward: `trittium-cli getmasternodestatus`

You need to get **"status" : 4**

## Congratulations your Trittium node is now running
