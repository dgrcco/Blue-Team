# Install and setup Splunk to learn for free

use [https://temp-mail.org](https://temp-mail.org) to create a trial account and download Splunk Enterprise.
Official installation: [https://help.splunk.com/en/splunk-enterprise/get-started/search-tutorial/9.3/part-1-getting-started/install-splunk-enterprise#id_0b0731b9_7ad0_4d56_8948_82c25ebc7105__Linux_installation_instructions](https://help.splunk.com/en/splunk-enterprise/get-started/search-tutorial/9.3/part-1-getting-started/install-splunk-enterprise#id_0b0731b9_7ad0_4d56_8948_82c25ebc7105__Linux_installation_instructions)


```
wget -O splunk-10.0.2-e2d18b4767e9-linux-amd64.tgz "https://download.splunk.com/products/splunk/releases/10.0.2/linux/splunk-10.0.2-e2d18b4767e9-linux-amd64.tgz"
sudo tar xvzf splunk-10.0.2-e2d18b4767e9-linux-amd64.tgz -C /opt
```

## Start Splunk Enterprise

```
cd /opt/splunk/bin/
sudo ./splunk start
```

choose your credentials.

## Login

ubuntu server IP (vmware): 192.168.163.131

web app 192.168.163.131:8000

![login](/../main/img/Immagine%202025-11-14%20191406.png)

![dashboard](/../main/img/Immagine%202025-11-14%20191508.png)


## Setup Https

setup tls [https://help.splunk.com/en/splunk-enterprise/administer/manage-users-and-security/9.0/secure-splunk-platform-communications-with-transport-layer-security-certificates/configure-splunk-web-to-use-tls-certificates#id_2771b640_5e98_4545_bbfe_8444e86bc31d__Configure_Splunk_Web_to_use_TLS_certificates](https://help.splunk.com/en/splunk-enterprise/administer/manage-users-and-security/9.0/secure-splunk-platform-communications-with-transport-layer-security-certificates/configure-splunk-web-to-use-tls-certificates#id_2771b640_5e98_4545_bbfe_8444e86bc31d__Configure_Splunk_Web_to_use_TLS_certificates)

go to https://192.168.163.131:8000/it-IT/manager/launcher/server/settings/settings?action=edit and turn on https.

go to http://192.168.163.131:8000/it-IT/manager/launcher/forwardreceive and set the port to receive the data.

## Install a set of data to study splunk

```
cd /opt/splunk/etc/apps
sudo wget https://botsdataset.s3.amazonaws.com/botsv3/botsv3_data_set.tgz
sudo tar xvf botsv3_data_set.tgz
sudo rm -rf botsv3_data_set.tgz
sudo chown -R test:test botsv3_data_set/
cd /opt/splunk/bin/
sudo ./splunk restart
```

![dataset](/../main/img/Immagine%202025-11-26%20173041.png)


## Setup Universal Forwarder

```
useradd -m splunkfwd
groupadd splunkfwd

export SPLUNK_HOME="/opt/splunkforwarder"
mkdir $SPLUNK_HOME
chown -R splunkfwd:splunkfwd $SPLUNK_HOME

cd $SPLUNK_HOME

wget -O splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.tgz "https://download.splunk.com/products/universalforwarder/releases/10.0.2/linux/splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.tgz"

tar -xvzf splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.tgz -C $SPLUNK_HOME --strip-components=1

sudo $SPLUNK_HOME/bin/splunk start --accept-license
cd /bin
./splunk enable listen 9997 -auth admin:password
```

Now, create an index for the receiver on the splunk enterprise.

### Configure the universal forwarder to connect to a receiving indexer

```
./splunk add forward-server <host name or ip address>:<listening port>
```

### Configure a data input on the forwarder

```
./splunk add monitor /var/log
```

