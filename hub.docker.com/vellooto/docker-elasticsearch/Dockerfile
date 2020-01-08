FROM centos:latest
LABEL mantainer="alexis.mura@gmail.com"

RUN yum update -y \
    && yum install -y wget

# Setup gosu for easier command execution
ENV GOSU_VERSION=1.10
RUN gpg --keyserver pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    && curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64" \
    && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64.asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && rm -r /root/.gnupg/ \
    && chmod +x /usr/local/bin/gosu

WORKDIR /opt

RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/server-jre-8u181-linux-x64.tar.gz" \
    && tar xvf server-jre-8u181-linux-x64.tar.gz \
    && ln -s jdk1.8.0_181 java \
    && rm server-jre-8u181-linux-x64.tar.gz

RUN useradd -m -s /bin/bash elasticsearch \
    && wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.0.0.tar.gz \
    && tar xvf elasticsearch-6.0.0.tar.gz \
    && ln -s elasticsearch-6.0.0 elasticsearch \
    && chown -RL elasticsearch.elasticsearch elasticsearch \
    && rm elasticsearch-6.0.0.tar.gz 
    
ENV JAVA_HOME=/opt/java

EXPOSE 9200
EXPOSE 9300

WORKDIR /root

ADD ["elasticsearch.yml", "/opt/elasticsearch/config/"]
ADD ["startup.sh", "."]

ENTRYPOINT ["./startup.sh"]
