# Monitoramento do Asterisk 16 (CentOS 7) via Zabbix v5.4

### Execute os camoandos abaixo no servidor Asterisk 16

-- rpm -Uvh "http://repo.zabbix.com/zabbix/5.4/rhel/7/x86_64/zabbix-release-5.4-1.el7.noarch.rpm"
- yum install -y "zabbix-agent" "jq"
- vim "/etc/zabbix/zabbix_agentd.conf"
- cp "/etc/zabbix/zabbix_agentd.conf" "/etc/zabbix/zabbix_agentd.conf.orig"
- sed -i 's/Server=127.0.0.1/Server=127.0.0.1,192.168.0.13/g' "/etc/zabbix/zabbix_agentd.conf"
- sed -i 's/Example: Server=127.0.0.1,192.168.0.13/Example: Server=127.0.0.1/g' "/etc/zabbix/zabbix_agentd.conf"
- sed -i 's/ServerActive=127.0.0.1/ServerActive=127.0.0.1,192.168.0.13/g' "/etc/zabbix/zabbix_agentd.conf"
- sed -i 's/Example: ServerActive=127.0.0.1,192.168.0.13/Example: ServerActive=127.0.0.1/g' "/etc/zabbix/zabbix_agentd.conf"
- sed -i 's/Hostname=Zabbix server/Hostname=Asterisk/g' "/etc/zabbix/zabbix_agentd.conf"
- systemctl restart "zabbix-agent"
- chkconfig "zabbix-agent" on
- yum install -y "git"
- wget "https://raw.githubusercontent.com/NoNAT-Telecom/Asterisk-16-Zabbix-v5.4/main/sip.discovery"
- wget "https://raw.githubusercontent.com/NoNAT-Telecom/Asterisk-16-Zabbix-v5.4/main/zabbix-asterisk.conf"
- wget "https://raw.githubusercontent.com/NoNAT-Telecom/Asterisk-16-Zabbix-v5.4/main/zabbix-asterisk.php"
- mkdir "/etc/zabbix/scripts"
- cp "sip.discovery" "/etc/zabbix/scripts/sip.discovery"
- cp "sip.discovery" "/etc/zabbix/scripts/sip.discovery.orig"
- cp "zabbix-asterisk.conf" "/etc/zabbix/zabbix_agentd.d/zabbix-asterisk.conf"
- cp "/etc/zabbix/zabbix_agentd.d/zabbix-asterisk.conf" "/etc/zabbix/zabbix_agentd.d/zabbix-asterisk.conf.orig"
- cp "zabbix-asterisk.php" "/var/local/zabbix-asterisk.php"
- cp "/var/local/zabbix-asterisk.php" "/var/local/zabbix-asterisk.php.orig"
- rm -f "sip.discovery"
- rm -f "zabbix-asterisk.conf"
- rm -f "zabbix-asterisk.php"
- chmod +x "/etc/zabbix/scripts/sip.discovery"
- chmod +x "/etc/zabbix/zabbix_agentd.d/zabbix-asterisk.conf"
- chmod +x "/var/local/zabbix-asterisk.php"
- echo "UnsafeUserParameters=1" >> "/etc/zabbix/zabbix_agentd.conf"
- echo "UserParameterDir=/etc/zabbix/zabbix_agentd.d/" >> "/etc/zabbix/zabbix_agentd.conf"
- systemctl restart "zabbix-agent"
