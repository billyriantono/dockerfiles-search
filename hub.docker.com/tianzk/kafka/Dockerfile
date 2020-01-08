FROM java:8-jre

# add our user and group first to make sure their IDs get assigned consistently
RUN groupadd -r kafka && useradd -r -g kafka kafka

# grab gosu for easy step-down from root
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN arch="$(dpkg --print-architecture)" \
	&& set -x \
	&& curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.3/gosu-$arch" \
	&& curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.3/gosu-$arch.asc" \
	&& gpg --verify /usr/local/bin/gosu.asc \
	&& rm /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu

ENV KAFKA_VERSION 0.8.2.1
ENV SCALA_VERSION 2.11
RUN wget -c -t 5 http://apache.fayea.com/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz && \
	tar -zxvf ./kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -C /usr/local && \
	rm ./kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz && \
	mv /usr/local/kafka_${SCALA_VERSION}-${KAFKA_VERSION} /usr/local/kafka && \
	chown kafka:kafka /usr/local/kafka

ENV PATH /usr/local/kafka/bin:$PATH

COPY ./docker-entrypoint.sh /

VOLUME /tmp/kafka-logs

EXPOSE 2181
EXPOSE 9092

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD []
