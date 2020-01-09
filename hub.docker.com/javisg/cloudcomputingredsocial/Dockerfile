
FROM debian:jessie-backports
MAINTAINER Javier Salido Gómez <javisago91@gmail.com> Version: 1.0 
 

 
# explicitly set user/group IDs 
RUN groupadd -r cassandra --gid=999 && useradd -r -g cassandra --uid=999 cassandra 

 
# grab gosu for easy step-down from root 
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \ 
&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \ 
&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \ 
&& gpg --verify /usr/local/bin/gosu.asc \ 
	&& rm /usr/local/bin/gosu.asc \ 
&& chmod +x /usr/local/bin/gosu \ 
	&& apt-get purge -y --auto-remove ca-certificates wget 
 
 
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 514A2AD631A57A16DD0047EC749D6EEC0353B12C 

 
RUN echo 'deb http://www.apache.org/dist/cassandra/debian 32x main' >> /etc/apt/sources.list.d/cassandra.list 

 
ENV CASSANDRA_VERSION 3.2 
 
 
 RUN apt-get update \ 
	&& apt-get install -y cassandra="$CASSANDRA_VERSION" \ 
	&& rm -rf /var/lib/apt/lists/* 
 
ENV CASSANDRA_CONFIG /etc/cassandra 



 
RUN mkdir -p /var/lib/cassandra "$CASSANDRA_CONFIG" \ 
&& chown -R cassandra:cassandra /var/lib/cassandra "$CASSANDRA_CONFIG" \ 
&& chmod 777 /var/lib/cassandra "$CASSANDRA_CONFIG" 
VOLUME /var/lib/cassandra 

 
EXPOSE 7000 7001 7199 9042 9160 
CMD ["cassandra", "-f"] 

