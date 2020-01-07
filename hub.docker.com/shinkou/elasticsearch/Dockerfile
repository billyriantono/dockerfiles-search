FROM shinkou/jre
RUN set -x \
	&& apt-get update \
	&& apt-get install -y gosu wget \
	&& cd /tmp \
	&& wget 'https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.7.deb' \
	&& dpkg -i elasticsearch-5.6.7.deb \
	&& apt-get clean -y
RUN echo 'http.host: 0.0.0.0' >> /etc/elasticsearch/elasticsearch.yml
ENV PATH /usr/share/elasticsearch/bin:$PATH

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 9200 9300
CMD ["elasticsearch", "-p", "/var/run/elasticsearch/elasticsearch.pid", "-Edefault.path.logs=/var/log/elasticsearch", "-Edefault.path.data=/var/lib/elasticsearch", "-Edefault.path.conf=/etc/elasticsearch"]
