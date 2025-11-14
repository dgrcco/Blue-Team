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


## Setup Splunk and Forwarder

[continue]
