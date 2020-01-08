FROM openjdk:8-jre

MAINTAINER Dmitry Kireev <dmitry@kireev.co>
USER root

ENV \
  DEBIAN_FRONTEND=noninteractive \
  TERM=xterm-color


ENV ELASTICSEARCH_VERSION 2.4.3
ENV ELASTICSEARCH_DEB_VERSION 2.4.3

ENV KIBANA_MAJOR 4.6
ENV KIBANA_VERSION 4.6.3

ENV LOGSTASH_VERSION 2.4.1
ENV LOGSTASH_DEB_VERSION 1:2.4.1-1

ENV CURATOR_MAJOR 4
ENV CURATOR_VERSION 4.1.2

# Install packages
RUN apt-get clean && apt-get update && apt-get install -my \
  supervisor \
  cron \
  python python-pip python-dev \
  htop vim strace dstat mc mysql-client netcat \
  wget \
  curl

# Install j2cli (will help us with config templating)
RUN pip install j2cli && pip install j2cli[yaml]


# Add configuration files
RUN mkdir -p /root/.docker/
ADD .docker/templates/ /root/.docker/templates/

# https://artifacts.elastic.co/GPG-KEY-elasticsearch
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 46095ACC8548582C1A2699A9D27D666CD88E42B4

################################################################################
# Base image
################################################################################

# Add app-env
ADD .docker/bin/app-env /usr/local/bin/app-env
RUN chmod a+x /usr/local/bin/app-env

# Add start
ADD .docker/bin/start /usr/local/bin/start
RUN chmod a+x /usr/local/bin/start

# Add configuration files
ADD .docker/templates/ /root/.docker/templates/


################################################################################
# Elasticsearch
################################################################################

# https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-repositories.html
# https://www.elastic.co/guide/en/elasticsearch/reference/5.0/deb.html
RUN set -x \
	&& apt-get update && apt-get install -y --no-install-recommends apt-transport-https && rm -rf /var/lib/apt/lists/* \
	&& echo 'deb http://packages.elasticsearch.org/elasticsearch/2.x/debian stable main' > /etc/apt/sources.list.d/elasticsearch.list


RUN set -x \
	\
# don't allow the package to install its sysctl file (causes the install to fail)
# Failed to write '262144' to '/proc/sys/vm/max_map_count': Read-only file system
	&& dpkg-divert --rename /usr/lib/sysctl.d/elasticsearch.conf \
	\
	&& apt-get update \
	&& apt-get install -y --no-install-recommends "elasticsearch=$ELASTICSEARCH_DEB_VERSION" \
	&& rm -rf /var/lib/apt/lists/*


ENV PATH /usr/share/elasticsearch/bin:$PATH
WORKDIR /usr/share/elasticsearch




################################################################################
# Logstash
################################################################################
RUN echo 'deb http://packages.elastic.co/logstash/2.4/debian stable main' > /etc/apt/sources.list.d/logstash.list
RUN set -x \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends "logstash=$LOGSTASH_DEB_VERSION" \
	&& rm -rf /var/lib/apt/lists/*

ENV PATH /opt/logstash/bin:$PATH
# necessary for 5.0+ (overriden via "--path.settings", ignored by < 5.0)
ENV LS_SETTINGS_DIR /etc/logstash

#RUN apt-get install --no-install-recommends -y logstash && \
#    apt-get clean
#
#
## Logstash plugins
#RUN /opt/logstash/bin/plugin install logstash-filter-translate
#
#ENV PATH /opt/logstash/bin:$PATH

################################################################################
# Kibana
################################################################################

RUN echo "deb http://packages.elastic.co/kibana/${KIBANA_MAJOR}/debian stable main" > /etc/apt/sources.list.d/kibana.list

RUN set -x \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends kibana=$KIBANA_VERSION \
	&& chown -R kibana:kibana /opt/kibana \
	&& rm -rf /var/lib/apt/lists/*
ENV PATH /opt/kibana/bin:$PATH


################################################################################
# Elastic Curator
################################################################################
RUN echo "deb http://packages.elastic.co/curator/${CURATOR_MAJOR}/debian stable main" > /etc/apt/sources.list.d/curator.list

RUN mkdir -p /root/.curator

RUN set -x \
	\
# don't allow the package to install its sysctl file (causes the install to fail)
# Failed to write '262144' to '/proc/sys/vm/max_map_count': Read-only file system
	&& dpkg-divert --rename /usr/lib/sysctl.d/elasticsearch.conf \
	\
	&& apt-get update \
	&& apt-get install -y --no-install-recommends "elasticsearch-curator=$CURATOR_VERSION" \
	&& rm -rf /var/lib/apt/lists/*


################################################################################
# Volumes
################################################################################

VOLUME ["/usr/share/elasticsearch/data", "/var/log/app", "/etc/logstash"]


################################################################################
# Ports
################################################################################

EXPOSE 9200 9300 5601 5044 1514

################################################################################
# Entrypoint
################################################################################

ENTRYPOINT ["/usr/local/bin/start"]

