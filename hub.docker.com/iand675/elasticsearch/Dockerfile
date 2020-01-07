FROM ubuntu
MAINTAINER Ian Duncan <ian@iankduncan.com>

#prepare for Java download
RUN apt-get install -y python-software-properties
RUN apt-get install -y software-properties-common

#grab oracle java (auto accept licence)
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java7-installer


ADD https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-0.90.7.deb /tmp/elasticsearch.deb
RUN dpkg -i /tmp/elasticsearch.deb
RUN rm /tmp/elasticsearch.deb
CMD /usr/share/elasticsearch/bin/elasticsearch -f
EXPOSE 9200 9300
VOLUME ["/usr/share/elasticsearch"]
