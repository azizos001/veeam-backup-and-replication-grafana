# veeam-backup-and-replication-grafana
 InfluxDB:
wget -qO- https://repos.influxdata.com/influxdb.key | sudo gpg --dearmor -o /usr/share/keyrings/influxdb.gpg
echo "deb [signed-by=/usr/share/keyrings/influxdb.gpg] https://repos.influxdata.com/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/influxdb.list

sudo apt update
sudo apt install influxdb
sudo systemctl enable --now influxdb

Grafana:
sudo apt install -y apt-transport-https software-properties-common wget
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list

sudo apt update
sudo apt install grafana
sudo systemctl enable --now grafana-server

jq and curl:
sudo apt install -y jq curl

Download the script:
wget https://raw.githubusercontent.com/VeeamHub/grafana/master/veeam-enterprise_manager-grafana/veeam_enterprisemanager.sh
chmod +x veeam_enterprisemanager.sh
Edit the script:
nano veeam_enterprisemanager.sh
Update the config section like this:
veeamUsername="your_veeam_username"
veeamPassword="your_veeam_password"
veeamRestServer="your_veeam_enterprise_manager_ip"
veeamRestPort="9398"
===================================================================================
veeamInfluxDBURL="http://localhost"
veeamInfluxDBPort="8086"
veeamInfluxDBDatabase="veeamdb"
Then run it:
./veeam_enterprisemanager.sh
=======================================================================================
1. Remove InfluxDB 1.8

sudo systemctl stop influxdb
sudo apt purge influxdb influxdb-client -y
sudo rm -rf /etc/influxdb /var/lib/influxdb /var/log/influxdb
⬇️ 2. Install InfluxDB 2.x (latest stable)

wget -qO- https://repos.influxdata.com/influxdata-archive_compat.key | sudo tee /etc/apt/keyrings/influxdata-archive_compat.key > /dev/null
echo 'deb [signed-by=/etc/apt/keyrings/influxdata-archive_compat.key] https://repos.influxdata.com/ubuntu jammy stable' | sudo tee /etc/apt/sources.list.d/influxdata.list
sudo apt update
sudo apt install influxdb2
sudo systemctl enable influxdb
sudo systemctl start influxdb
⚙️ 3. Access InfluxDB UI and Set It Up
Go to:
http://192.168.50.170:8086
On first launch:
Choose a username and password
Set your organization name (e.g., veeam_org)
Set your bucket name (e.g., veeam)
It will give you a token — copy and save it
✅ 4. Download the Correct Script

wget https://raw.githubusercontent.com/VeeamHub/grafana/master/veeam-enterprise_manager-grafana/influxdb-v2.0/veeam-enterprisemanager.sh
chmod +x veeam-enterprisemanager.sh


E: Conflicting values set for option Signed-By regarding source https://repos.influxdata.com/ubuntu/ jammy: /etc/apt/keyrings/influxdata-archive_compat.key != /usr/share/keyrings/influxdb.gpg
E: The list of sources could not be read.
///////////////
sudo rm /etc/apt/sources.list.d/influxdb.list 2>/dev/null
sudo rm /usr/share/keyrings/influxdb.gpg 2>/dev/null
/////////////////////
sudo rm /etc/apt/sources.list.d/influxdata.list 2>/dev/null
////////////////////
wget -qO- https://repos.influxdata.com/influxdata-archive_compat.key | sudo tee /etc/apt/keyrings/influxdata-archive_compat.key > /dev/null

echo 'deb [signed-by=/etc/apt/keyrings/influxdata-archive_compat.key] https://repos.influxdata.com/ubuntu jammy stable' | \
sudo tee /etc/apt/sources.list.d/influxdata.list
/////////////////
sudo apt update
sudo apt install influxdb2
//////////////
sudo systemctl enable influxdb
sudo systemctl start influxdb

