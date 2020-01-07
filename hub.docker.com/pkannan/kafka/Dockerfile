FROM pkannan/java8:latest

ENV VERSION=1.0.0 SCALAVERSION=2.12 MIRROR=http://apache.mirrors.pair.com/ \
    USER_ID=1000 USER=kafka

RUN	wget -q -O - "$MIRROR/kafka/$VERSION/kafka_$SCALAVERSION-$VERSION.tgz" | tar -xzf - -C /opt \
	&& mv "/opt/kafka_$SCALAVERSION-$VERSION" /opt/kafka

COPY conf/config-kafka.sh /opt/kafka/bin

RUN chmod +x /opt/kafka/bin/config-kafka.sh \
	&& groupadd -r $USER --gid=$USER_ID && useradd -r -g $USER --uid=$USER_ID $USER 

ENTRYPOINT ["/opt/kafka/bin/config-kafka.sh"]

RUN chown -R $USER:$USER /opt/kafka 
USER $USER
WORKDIR /opt/kafka
EXPOSE 9092
VOLUME ["/opt/kafka/data", "/opt/kafka/log"]
CMD ["/opt/kafka/bin/kafka-server-start.sh", "/opt/kafka/config/server.properties"]
