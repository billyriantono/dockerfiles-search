FROM zabbix/zabbix-appliance:ubuntu-3.4-latest
RUN apt update
RUN apt-get install -y curl git
RUN git clone https://github.com/yuri-karpovich/slack-alert-from-bash-and-zabbix.git
COPY ["my_entrypoint.sh", "/usr/bin/"]
RUN chmod +x /usr/bin/my_entrypoint.sh

ENTRYPOINT ["my_entrypoint.sh"]



