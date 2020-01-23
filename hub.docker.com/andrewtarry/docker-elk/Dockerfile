FROM java:8
MAINTAINER Andrew Tarry <andrew@andrewtarry.com>

RUN apt-get update && apt-get install -y wget supervisor

RUN wget -qO - https://packages.elasticsearch.org/GPG-KEY-elasticsearch | apt-key add -
RUN echo "deb http://packages.elasticsearch.org/elasticsearch/1.5/debian stable main" | tee -a /etc/apt/sources.list
RUN echo "deb http://packages.elasticsearch.org/logstash/1.4/debian stable main" | tee -a /etc/apt/sources.list
RUN apt-get update && apt-get install -y elasticsearch logstash && apt-get clean
ENV PATH /usr/share/elasticsearch/bin:$PATH
ADD config/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml
ADD config/logstash.conf /opt/logstash.conf

VOLUME /usr/share/elasticsearch/data

RUN wget https://download.elasticsearch.org/kibana/kibana/kibana-4.0.1-linux-x64.tar.gz
RUN tar -C /opt -zxvf kibana-4.0.1-linux-x64.tar.gz
ADD config/kibana.yml /opt/kibana-4.0.1-linux-x64/config/kibana.yml
RUN ln -s /opt/kibana-4.0.1-linux-x64 /opt/kibana
RUN rm kibana-4.0.1-linux-x64.tar.gz

ADD supervisor/logstash.conf /etc/supervisor/conf.d/logstash.conf
ADD supervisor/kibana.conf /etc/supervisor/conf.d/kibana.conf
ADD supervisor/elasticsearch.conf /etc/supervisor/conf.d/elasticsearch.conf

EXPOSE 5601 9200

CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]
