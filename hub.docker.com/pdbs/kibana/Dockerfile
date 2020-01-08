FROM ubuntu:latest
LABEL build="201911221440" kibana.version="7.4.2"
LABEL maintainer "marc.jakob@bs.ch"

COPY dpkg-excludes /etc/dpkg/dpkg.cfg.d/excludes
COPY start.sh /

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get -y install locales gnupg wget apt-transport-https && \
    locale-gen en_US.UTF-8 && \
    locale-gen de_CH.UTF-8 && \
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add - && \
    echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list && \
    apt-get update && \
    apt-get install kibana && \
    apt-get -y purge gnupg wget apt-transport-https && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo "server.host: \"0.0.0.0\"" >> /etc/kibana/kibana.yml && \
    echo "elasticsearch.hosts: \"http://elasticsearch:9200\"" >> /etc/kibana/kibana.yml && \
    chmod 0750 /start.sh

EXPOSE 5601
ENTRYPOINT ["/start.sh"]
