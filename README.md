piWallet
========

piWallet is a popular secure opensource online altcoin wallet that works with practically any altcoin. piWallet uses PHP, mySQL, JavaScript and Bootstrap meaning it's quite simple to setup. 

Setup: https://github.com/johnathanmartin/piWallet/wiki/Installation

TODO: Add a step in the wiki explaining to copy settings-example.php into a new file settings.php and then change the values.

Bitcoin Talk Thread: https://bitcointalk.org/index.php?topic=911212

Please exercise EXTREME CAUTION when having a 3rd party install piWallet, please see https://fittechhosting.com/cryptocurrency for approved installation/piWallet hosting services. 

I can be reached directly at jmartin@FitTechHosting.com

Features:

- Manual User Reserve

- QR Codes use a local generation URL 

- Multilanguage support for over 90% of text - Currently supported languages include English, Greek, Mandarin, Hindi, Italian, Portuguese, Spanish, and Tagalog.

- QR Codes for Addresses

- Google 2 Factor Auth

- Mobile App (Additional Addon - see https://FitTechHosting.com/cryptocurrency )

- Fee Sent to Wallet Owner (Included w/ Hosting - https://FitTechHosting.com/cryptocurrency)

Planned Features:

- Have QR Codes open in lightbox instead of new tab

- Control of Private Keys

- Improved Bootstrap Theme 

Todo List:

- Issue #78 - PHP Juggling 

- Issue #82 - Strip tags bug

- Issue #83 - change default password from changeme

- Issue #36  Stop using md5

- Change background from ugly yellow

 
More Information:

Created by Johnathan Martin of FitTechHosting.com


Use the following tutorial to setup a web wallet for a Scrypt PoW/PoS coin.

Make sure that you have the following requirements.

- A server or VPS.
- A domain. (This tutorial uses the domain example.com)
- A hostname pointed to your VPS. (This tutorial uses the hostname wallet.example.com)

Update your Ubuntu machine.

sudo apt-get update
sudo apt-get upgrade

Install the required dependencies.

sudo apt-get install libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libdb-dev libdb++-dev libminiupnpc-dev git nano

Go to your home directory.

cd $HOME

Note: replace “examplecoin” with the name of your coin.
Note: replace “6gs39011kick8xmqutpkrvi92xx5kwev4ykanlv1ls0ouuae5x” with the coinID of your coin.

Download the daemon from MyCoin. (Available for a paid coin)

wget "https://dl.walletbuilders.com/download?customer=6gs39011kick8xmqutpkrvi92xx5kwev4ykanlv1ls0ouuae5x&filename=examplecoin-daemon-linux.tar.gz" -O examplecoin-daemon-linux.tar.gz

Extract the tar files.

tar -xzvf examplecoin-daemon-linux.tar.gz

Install the daemon and tools.

sudo mv examplecoind /usr/bin/

Create the config file.

mkdir $HOME/.examplecoin
nano $HOME/.examplecoin/examplecoin.conf

Paste the following lines in examplecoin.conf.

rpcuser=rpc_examplecoin
rpcpassword=CQRMSKLFUikEppUzKNbR7tGFKPMq3zhlS3eBUp2f
rpcallowip=127.0.0.1
listen=1
server=1
txindex=1
daemon=1
enableaccounts=1
staking=0

Start your daemon with the following command.

examplecoind

Show your donate address.

examplecoind getaccountaddress "donate"

Example output

TLWgVeFEUJyWrRW7jccU5oh9j3i65ohQne

Keep note of the donate address.

Install PHP 5.6.
sudo add-apt-repository -y ppa:ondrej/php
sudo apt-get update
sudo apt-get install git apache2 php5.6 php5.6-mysql php5.6-gd libapache2-mod-php5.6 mysql-server

Go to your home directory.

cd $HOME

Download piWallet.

sudo git clone https://github.com/johnathanmartin/piWallet/

Move piWallet to the www directory.

sudo mv piWallet/* /var/www/html/

Open MySQL.

sudo mysql

Create the database “wallet”.

CREATE DATABASE wallet;

Note: replace the value “Ee4cxBN6VaThkAr4fKigzWR7veDPZlvU1dVzYg4H” with a unique password.
Create the database user.

CREATE USER 'wallet_user'@'localhost' IDENTIFIED BY 'Ee4cxBN6VaThkAr4fKigzWR7veDPZlvU1dVzYg4H';

Give the user “wallet_user” rights to the database “wallet”.

GRANT ALL PRIVILEGES ON wallet.* TO 'wallet_user'@'localhost';

Open the database “wallet”.

USE wallet;

Copy and paste the content of the file users.sql.

Close mysql.

quit;

Create Google reCAPTCHA keys
Open a new tab in your browser and go to https://www.google.com/recaptcha

Login with your Google account.

To register a new site, click the plus sign in the top right corner.

Register new site Google reCAPTCHA
Fill-in the form.

Label - A label to identify your site.

reCAPTCHA type - Select the option “reCAPTCHA v2”.

Domains - Enter the domain that you will use to access your web wallet.

Register new site Google reCAPTCHA example form
Accept the reCAPTCHA Terms of Service and click on the button “submit” to register your site.
Your reCAPTCHA site and secret key will be visible on the next page once the site is registered.

Example reCAPTCHA keys.

Google reCAPTCHA example keys


Configure piWallet
Create the settings file.

sudo cp /var/www/html/settings-example.php /var/www/html/settings.php

Open the settings file.

sudo nano /var/www/html/settings.php

Change the marked values.

$db_user - Change the value “root” with the value “wallet_user”.

$db_pass - Change the value “password” with the MySQL password of the user “wallet_user”.

$rpc_port - Change the value “8332” with the RPC port of your coin.

$rpc_user - Change the value “bitcoinrpc” with the RPC username of your coin.

$rpc_pass - Change the value “Cp68nBkCAADKkskaKSskaDKdmSYLtLJ” with the RPC password of your coin.

$fullname - Change the value “Bitcoin” with the name of your coin.

$short - Change the value “BTC” with the abbreviation of your coin.

$blockchain_tx_url - Change the value “http://blockchain.info/tx/” with the URL to your block explorer.

$support - Change the value “support@yourwebsite.com” with your support email address.

$donation_address - Fill in your donate address.

$public - Change the value “Recaptcha_publickey_here” with your reCAPTCHA site key.

$secret - Change the value “Recaptcha_privatekey_here” with your reCAPTCHA secret key.


Original settings.php.


$server_url = "/";  // ENTER WEBSITE URL ALONG WITH A TRAILING SLASH

$db_host = "localhost";
$db_user = "root";
$db_pass = "password";
$db_name = "wallet";

$rpc_host = "127.0.0.1";
$rpc_port = "8332";
$rpc_user = "bitcoinrpc";
$rpc_pass = "Cp68nBkCAADKkskaKSskaDKdmSYLtLJ";

$fullname = "Bitcoin"; //Website Title (Do Not include 'wallet')
$short = "BTC"; //Coin Short (BTC)
$blockchain_tx_url = "http://blockchain.info/tx/"; //Blockchain Url
$support = "support@yourwebsite.com"; //Your support eMail
$hide_ids = array(1); //Hide account from admin dashboard
$donation_address = ""; //Donation Address

$reserve = "0";
//Recaptcha
$public = "Recaptcha_publickey_here";
$secret = "Recaptcha_privatekey_here";

Example settings.php.


$server_url = "/";  // ENTER WEBSITE URL ALONG WITH A TRAILING SLASH

$db_host = "localhost";
$db_user = "wallet_user";
$db_pass = "Ee4cxBN6VaThkAr4fKigzWR7veDPZlvU1dVzYg4H";
$db_name = "wallet";

$rpc_host = "127.0.0.1";
$rpc_port = "5303";
$rpc_user = "rpc_examplecoin";
$rpc_pass = "CQRMSKLFUikEppUzKNbR7tGFKPMq3zhlS3eBUp2f";

$fullname = "Examplecoin"; //Website Title (Do Not include 'wallet')
$short = "EXP"; //Coin Short (BTC)
$blockchain_tx_url = "https://example.com/tx/"; //Blockchain Url
$support = "support@example.com"; //Your support eMail
$hide_ids = array(1); //Hide account from admin dashboard
$donation_address = "TLWgVeFEUJyWrRW7jccU5oh9j3i65ohQne"; //Donation Address

$reserve = "0";
//Recaptcha
$public = "6Ld4xbIUAAAAAAOPOy-LXu6PPXsgHCFoEwmNM23S";
$secret = "6Ld4xbIUAAAAAJEyaKkZV0TSccnwFTEpZMh987KK";

Save the settings file.

Remove the default index.html file.

sudo rm /var/www/html/index.html

Install Let’s Encrypt.

sudo add-apt-repository universe && sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update && sudo apt-get install certbot python-certbot-apache

Create a SSL certificate.

sudo certbot --apache

Enter your support email address.

Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel):
support@example.com

Agree with the Let's Encrypt Terms of Service.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v02.api.letsencrypt.org/directory
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(A)gree/(C)ancel:
Press a and enter to agree to the Terms of Service.


Agree to share your email address with Let's Encrypt.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about our work
encrypting the web, EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o:
Press n and enter to not share your email address.


Enter the hostname of your server.

No names were found in your configuration files. Please enter in your domain
name(s) (comma and/or space separated)  (Enter 'c' to cancel):
wallet.example.com

Redirect HTTP traffic to HTTPS.

Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel):
Press 2 and enter to redirect HTTP traffic to HTTPS.


Test your SSL configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=wallet.example.com

Test if you SSL certificate can be renewed using the following command:

sudo certbot renew --dry-run

Start a browser on your computer and open the page https://wallet.example.com

Use the following credentials to login.

Username - piWallet
Password - changeme

Note: Immediately change the password “changeme” with a strong and unique password.


