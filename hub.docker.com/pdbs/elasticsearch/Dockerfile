FROM ubuntu:latest
LABEL build="201911221445" elasticsearch.version="7.4.2"
LABEL maintainer "marc.jakob@bs.ch"

COPY dpkg-excludes /etc/dpkg/dpkg.cfg.d/excludes

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get -y install locales gnupg wget apt-transport-https openjdk-8-jre-headless && \
    locale-gen en_US.UTF-8 && \
    locale-gen de_CH.UTF-8 && \
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add - && \
    echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list && \
    apt-get update && \
    apt-get install elasticsearch && \
    apt-get -y purge wget apt-transport-https && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo "transport.host: localhost" >> /etc/elasticsearch/elasticsearch.yml && \
    echo "network.host: 0.0.0.0" >> /etc/elasticsearch/elasticsearch.yml && \
    sed -i "s/-d -p \$PID_FILE/-p \$PID_FILE/" /etc/init.d/elasticsearch

COPY start.sh /

RUN chmod 0750 /start.sh

EXPOSE 9200
ENTRYPOINT ["/start.sh"]
