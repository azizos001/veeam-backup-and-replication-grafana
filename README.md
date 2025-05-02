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

veeamInfluxDBURL="http://localhost"
veeamInfluxDBPort="8086"
veeamInfluxDBDatabase="veeamdb"
Then run it:
./veeam_enterprisemanager.sh

