FROM faboulaye/openjdk:alpine
MAINTAINER Firdaws Aboulaye "aboufred@gmail.com"

ARG KAFKA_VERSION=0.10.1.1
ARG KAFKA_MIRROR=http://www-eu.apache.org
ARG KAFKA_SCALA_VERSION=2.11
ENV KAFKA_HOME /opt/kafka

COPY docker-entrypoint.sh /

RUN apk --update add --no-cache wget bash\
  && mkdir /opt \
  && wget -q -O - $KAFKA_MIRROR/dist//kafka/$KAFKA_VERSION/kafka_$KAFKA_SCALA_VERSION-$KAFKA_VERSION.tgz  | tar -xzf - -C /opt \
  && mv /opt/kafka_* $KAFKA_HOME \
  && addgroup -S kafka \
  && adduser -S -u 200 -G kafka -h $KAFKA_HOME -s /bin/false kafka \
  && mkdir $KAFKA_HOME/data /var/log/kafka \
  && chown -R kafka:kafka $KAFKA_HOME \
  && chown -R kafka:kafka /var/log/kafka \
  && chmod a+x docker-entrypoint.sh \
  && apk del wget \
  && rm -rf /tmp/* /var/cache/* /usr/share/man/?? /usr/share/man/??_* /var/lib/apt/lists/* \

USER kafka
EXPOSE 9092
VOLUME ["/opt/kafka/data", "/opt/kafka/config"]
WORKDIR $KAFKA_HOME

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["bash"]
