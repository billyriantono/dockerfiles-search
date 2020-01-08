FROM mysql:5.7
ADD sql /sql
ADD zabbix-db-init.sh /docker-entrypoint-initdb.d/zabbix-db-init.sh
RUN chmod +x /docker-entrypoint-initdb.d/zabbix-db-init.sh
EXPOSE 3306
