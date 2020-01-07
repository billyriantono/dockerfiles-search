FROM netknight/java
MAINTAINER Jevgeni Goloborodko <jevgeni@digital-magic.io>

# Update apt repository and install elasticsearch & logstash
RUN wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - && \
	echo "deb http://packages.elastic.co/elasticsearch/2.x/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-2.x.list && \
	echo "deb http://packages.elastic.co/logstash/2.2/debian stable main" | sudo tee -a /etc/apt/sources.list

RUN sudo apt-get update && sudo apt-get --no-install-recommends -y install elasticsearch logstash && apt-get clean

# Elastic search plugins
RUN /usr/share/elasticsearch/bin/plugin install royrusso/elasticsearch-HQ
RUN /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head

# Logstash plugins
RUN /opt/logstash/bin/plugin install logstash-filter-translate

# Install kibana
RUN curl -s https://download.elastic.co/kibana/kibana/kibana-4.4.0-linux-x64.tar.gz | tar -C /opt -xz && \
    ln -s /opt/kibana-4.4.0-linux-x64 /opt/kibana

ENV PATH /opt/logstash/bin:$PATH

# Update services configuration
RUN echo "network.host: 0.0.0.0" >> /etc/elasticsearch/elasticsearch.yml
ADD ls.conf /etc/logstash/conf.d/logstash.conf
ADD kibana-init /etc/init.d/kibana
ADD kibana-default /etc/default/kibana

# Create kibana user and update file permissions
ENV KIBANA_HOME /opt/kibana
RUN chmod +x /etc/init.d/kibana && groupadd -r kibana && \
    useradd -r -s /usr/sbin/nologin -d ${KIBANA_HOME} -c "Kibana service user" -g kibana kibana && \
    mkdir -p /var/log/kibana && \
    chown -R kibana:kibana /opt/kibana-4.4.0-linux-x64 ${KIBANA_HOME} /var/log/kibana

# Supervisord configuration
#ADD elasticsearch.conf /etc/supervisor/conf.d/elasticsearch.conf
#ADD logstash.conf /etc/supervisor/conf.d/logstash.conf
#ADD kibana.conf /etc/supervisor/conf.d/kibana.conf
#CMD [ "/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf" ]

ADD ./start.sh /usr/local/bin/start.sh
RUN chmod +x /usr/local/bin/start.sh
CMD [ "/usr/local/bin/start.sh" ]

EXPOSE 5601 9200 9300 5000 5044
VOLUME /var/lib/elasticsearch