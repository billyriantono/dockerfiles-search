FROM debian:jessie
MAINTAINER Shan <shanmuga_karna@yahoo.com>

RUN apt-get update && \
    apt-get -y upgrade && \
	apt-get install -y curl default-jre-headless

RUN curl -sLO https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.1.deb && \
    dpkg -i elasticsearch-1.7.1.deb && \
    /usr/share/elasticsearch/bin/plugin -install mobz/elasticsearch-head && \
	/usr/share/elasticsearch/bin/plugin -install lmenezes/elasticsearch-kopf
	
ADD start /start	
RUN	chmod +x /start

EXPOSE 9200/tcp 9300/tcp
CMD ["/bin/sh" "-c" "/start"]                                                                                                                                                                                                                                                           
