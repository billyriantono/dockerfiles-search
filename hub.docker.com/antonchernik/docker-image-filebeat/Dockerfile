FROM antonchernik/docker-image-ubuntu:18.04

FROM antonchernik/docker-image-ubuntu:18.04


RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get -y install \
      openjdk-8-jre-headless \
      gosu \
      --no-install-recommends




ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV JRE_HOME /usr/lib/jvm/java-8-openjdk-amd64/jre


# https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-repositories.html
# https://www.elastic.co/guide/en/elasticsearch/reference/5.0/deb.html
RUN set -x \
	&& echo 'deb https://artifacts.elastic.co/packages/6.x/apt stable main' > /etc/apt/sources.list.d/elasticsearch.list

ENV FILEBEAT_VERSION 6.4.3
ENV FILEBEAT_DEB_VERSION 6.4.3

RUN set -x \
    && wget -O GPG-KEY-elasticsearch https://artifacts.elastic.co/GPG-KEY-elasticsearch \
    && apt-key add ./GPG-KEY-elasticsearch


RUN set -x \
	\
	&& dpkg-divert --rename /usr/lib/sysctl.d/filebeat.conf \
	\
	&& apt-get update \
	&& apt-get install -y --no-install-recommends "filebeat=$FILEBEAT_DEB_VERSION" \
	&& rm -rf /var/lib/apt/lists/*


ENV PATH /usr/share/filebeat/bin:$PATH

WORKDIR /usr/share/filebeat




COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
CMD ["/usr/local/bin/docker-entrypoint.sh"]