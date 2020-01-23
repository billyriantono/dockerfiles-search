FROM java:openjdk-7u65-jdk

MAINTAINER Helmy El-Tobgy "hel.my"

RUN groupadd -r bamboo && useradd -r -g bamboo bamboo

RUN apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*

RUN curl -o /usr/local/bin/gosu -SL 'https://github.com/tianon/gosu/releases/download/1.1/gosu' \
    && chmod +x /usr/local/bin/gosu

ENV BAMBOO_VERSION 5.6.2

RUN curl -SL "http://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-$BAMBOO_VERSION.tar.gz" -o /tmp/atlassian-bamboo.tar.gz \
    && mkdir -p /opt/atlassian/bamboo \
    && tar -xzf /tmp/atlassian-bamboo.tar.gz -C /opt/atlassian/bamboo --strip-components=1 \
    && rm /tmp/atlassian-bamboo.tar.gz
    

ENV BAMBOO_HOME /var/atlassian/bamboo/data
VOLUME /var/atlassian/bamboo/data

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 8085 54663

CMD ["/opt/atlassian/bamboo/bin/catalina.sh","run"]
