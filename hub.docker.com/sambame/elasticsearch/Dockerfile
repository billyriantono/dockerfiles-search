FROM charliek/openjdk-jre-7
MAINTAINER Shay Erlichmen "shay@samba.me"

RUN DEBIAN_FRONTEND=noninteractive apt-get install -yqq curl sudo
RUN curl http://packages.elasticsearch.org/GPG-KEY-elasticsearch | apt-key add -
RUN echo "deb http://packages.elasticsearch.org/elasticsearch/1.3/debian stable main" >> /etc/apt/sources.list
RUN apt-get -qq update && DEBIAN_FRONTEND=noninteractive apt-get install -y elasticsearch=1.3.4
RUN /usr/share/elasticsearch/bin/plugin -install elasticsearch/elasticsearch-cloud-gce/2.3.0

ADD run /usr/local/bin/run
ADD elasticsearch.yml /etc/elasticsearch/elasticsearch.yml
RUN chmod +x /usr/local/bin/run

EXPOSE 9200 9300
VOLUME ["/var/lib/elasticsearch"]
CMD ["/usr/local/bin/run"]