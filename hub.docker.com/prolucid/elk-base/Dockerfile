FROM phusion/baseimage
MAINTAINER Daniel Covello 

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

ENV KIBANA_VERSION 4.3.0

# Install ELK Required Dependancies
RUN set -x \
  && apt-get -qq update \
  && apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 46095ACC8548582C1A2699A9D27D666CD88E42B4 \
  && echo "deb http://packages.elastic.co/elasticsearch/2.x/debian stable main" >> /etc/apt/sources.list \
  && echo "deb http://packages.elasticsearch.org/logstash/2.0/debian stable main" >> /etc/apt/sources.list \
  && apt-get -qq update && apt-get -qy install openjdk-7-jre \
                                               elasticsearch \
                                               apache2-utils \
                                               supervisor \
                                               logstash \
                                               nginx --no-install-recommends \
  && apt-get purge -y --auto-remove wget \
  && apt-get clean \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& echo "Creating Elasticsearch Paths..." \
	&& for path in \
		/usr/share/elasticsearch/data \
		/usr/share/elasticsearch/logs \
		/usr/share/elasticsearch/config \
		/usr/share/elasticsearch/config/scripts \
	; do \
	mkdir -p "$path"; \
	done

# Install Kibana and Configure Nginx
ADD https://download.elastic.co/kibana/kibana/kibana-$KIBANA_VERSION-linux-x64.tar.gz /opt/
ADD config/nginx/kibana.conf /etc/nginx/sites-available/
# Configure Nginx
RUN cd /opt \
	&& echo "Installing Kibana "$KIBANA_VERSION"..." \
	&& tar xzf kibana-$KIBANA_VERSION-linux-x64.tar.gz \
	&& ln -s /opt/kibana-$KIBANA_VERSION-linux-x64 /opt/kibana \
	&& rm kibana-$KIBANA_VERSION-linux-x64.tar.gz \
	&& echo "Configuring Nginx..." \
	&& mkdir -p /var/www \
	&& echo "\ndaemon off;" >> /etc/nginx/nginx.conf \
	&& rm /etc/nginx/sites-enabled/default \
	&& ln -s /etc/nginx/sites-available/kibana.conf /etc/nginx/sites-enabled/kibana.conf

# Set permissions
RUN for path in \
		/usr/share/elasticsearch/data \
		/usr/share/elasticsearch/logs \
		/usr/share/elasticsearch/config \
		/usr/share/elasticsearch/config/scripts \
	; do \
	mkdir -p "$path"; \
	chown -R elasticsearch:elasticsearch "$path"; \
	done 

# Install Elasticsearch Curator
RUN apt-get update && apt-get install -y wget \
	&& wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - \
	&& echo "deb http://packages.elastic.co/curator/3/debian stable main" >> /etc/apt/sources.list \
	&& apt-get update && apt-get install -y python-elasticsearch-curator

# Add Elasticsearch config files
ADD config/elastic/* /usr/share/elasticsearch/config/
RUN chown elasticsearch:elasticsearch /usr/share/elasticsearch/config/*

# Add Logstash configuration file 
ADD config/main.conf /etc/logstash/main.conf

# Install Timelion Kibana Plugin
RUN /opt/kibana/bin/kibana plugin -i kibana/timelion

# Add nginx account 
COPY config/nginx/htpasswd /etc/nginx/.htpasswd

# Add ELK PATHs
ENV PATH /usr/share/elasticsearch/bin:$PATH
ENV PATH /opt/logstash/bin:$PATH
ENV PATH /opt/kibana/bin:$PATH

# Add Startup service scripts
RUN mkdir -p /etc/service/kibana
ADD config/service/start-kibana.sh /etc/service/kibana/run
RUN chmod +x /etc/service/kibana/run
RUN mkdir -p /etc/service/elasticsearch
ADD config/service/start-elasticsearch.sh /etc/service/elasticsearch/run
RUN chmod +x /etc/service/elasticsearch/run
RUN mkdir -p /etc/service/logstash
ADD config/service/start-logstash.sh /etc/service/logstash/run
RUN chmod +x /etc/service/logstash/run
RUN mkdir -p /etc/service/nginx
ADD config/service/start-nginx.sh /etc/service/nginx/run
RUN chmod +x /etc/service/nginx/run

VOLUME ["/usr/share/elasticsearch/data"]
VOLUME ["/etc/logstash/conf.d"]
VOLUME ["/etc/nginx"]

EXPOSE 80 443 9200 9300
