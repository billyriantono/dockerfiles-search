FROM ubuntu:15.10
MAINTAINER shanmugakarna<shanmuga_karna@yahoo.com>

#Oracle Java 8
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y python-software-properties software-properties-common wget vim curl && \
    add-apt-repository -y ppa:webupd8team/java && \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get update && apt-get install -y oracle-java8-installer
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

#ElasticSearch
RUN wget https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.3.deb && \
    dpkg -i elasticsearch-1.7.3.deb && \
    /usr/share/elasticsearch/bin/plugin -install mobz/elasticsearch-head && \
    /usr/share/elasticsearch/bin/plugin -install lmenezes/elasticsearch-kopf && \
    /usr/share/elasticsearch/bin/plugin install elasticsearch/elasticsearch-cloud-aws/2.5.0
EXPOSE 9200 9300

ENV ES_CLUSTER_NAME ElasticSearch

#Add start command
ADD start /start 
RUN chmod +x /start
CMD /start
