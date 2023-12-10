Playbook autoinstaller Prometheus and Grafana on Ubuntu/Debian 20.04/23.04.

Requirements:
Master node:
- nano
- git
- ansible
- generated private ssh key

Slave node:
- generated from master node ssh public key


Launch step by step on Master Node:
1. apt update -y 
2. sudo apt install git
3. sudo apt install software-properties-common
4. sudo add-apt-repository --yes --update ppa:ansible/ansible
5. sudo apt install ansible
6. git clone -b master git@github.com:Black872/ansible.git practice/prometheus | cd prometheus
7. nano hosts.txt # add DNS/ip address of your slave node
8. nano group_vars/DEV # change ansible_user and sudo pass on your user_name and sudo_pass_user_name
9. ansible-playbook prommanual.yml # will start installing Prometheus and then Grafana on slave nodes in hosts.txt
10. go on Grafana web http://slavenodeip:3000 and add first datasource Prometheus, then import dashboard with id 1860 Node Exporter Full

Config address:
http://slavenodeip:3000 # Grafana | configure grafana config in /prometheus/files/graffiles/
http://slavenodeip:9090 # Prometheus | configure prometheus config in /prometheus/files/promfiles/prometheus.yml
http://slavenodeip:9200 # Node_exporter | configure your targets in /prometheus/files/promfiles/prometheus.yml

You have now configured a node_exporter, from which prometheus scrapes data and visualizes target state graphs in grafana.