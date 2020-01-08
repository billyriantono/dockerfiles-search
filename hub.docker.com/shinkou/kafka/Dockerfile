FROM shinkou/jre
RUN set -x \
	&& apt update \
	&& apt-get install -y wget \
	&& apt-get clean -y
RUN set -x \
	&& cd /tmp \
	&& wget 'https://archive.apache.org/dist/kafka/0.10.0.1/kafka_2.11-0.10.0.1.tgz' \
	&& tar -zxvf ./kafka_2.11-0.10.0.1.tgz -C /usr/local/lib/ \
	&& ln -s /usr/local/lib/kafka_2.11-0.10.0.1 /usr/local/lib/kafka
ENV PATH $PATH:/usr/local/lib/kafka/bin

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 2181
CMD ["kafka"]
