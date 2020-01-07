#Zookeeper

FROM aviata/ubuntu

#Install zookeeper
RUN date -u +"%Y-%m-%d %H:%M%S?" && apt-get update \
    && date -u +"%Y-%m-%d %H:%M%S?" && apt-get install -y zookeeper wget supervisor dnsutils \
    && date -u +"%Y-%m-%d %H:%M%S?" && rm -rf /var/lib/apt/lists/* 

#Supervisor config
ADD supervisor/zookeeper.conf /etc/supervisor/conf.d/zookeeper.conf 

EXPOSE 2181

VOLUME ["/opt/zookeeper"]

CMD ["supervisord", "-n"]


