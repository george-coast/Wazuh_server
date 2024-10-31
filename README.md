The following is the set up for ip-based locations, which will be a reference, for iptables to use on theu ubuntu server to block certian ip address based on the location.

Install the required packages: 

sudo apt update
sudo apt install xtables-addons-common


Create a database for the ip address singuature:

sudo mkdir -p /usr/share/xt_geoip

Download the databasse:


cd /tmp
wget https://github.com/george-coast/Wazuh_server/raw/refs/heads/main/GeoLite2-Country.tar.gz

wget https://github.com/george-coast/Wazuh_server/raw/refs/heads/main/dbip-country-lite-2024-10.csv.gz


Extract the downloaded file: 


tar -xvzf GeoLite2-Country.tar.gz

gunzip dbip-country-lite-2024-10.csv.gz

mv dbip-country-lite-2024-10.csv dbip-country-lite.csv


Load the module

sudo modprobe xt_geoip



Example IP table entry:

sudo iptables -A INPUT -m geoip --src-cc CN -j DROP                > drops connections from China 


Install iptables-presistent | Save the current confiuration. 

sudo apt install iptables-persistent

sudo netfilter-persistent save


