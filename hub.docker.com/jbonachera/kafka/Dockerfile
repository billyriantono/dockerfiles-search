FROM jbonachera/arch

ENTRYPOINT ["/sbin/entrypoint"]
VOLUME ["/var/log/kafka"]
RUN pacman -S --noconfirm jre7-openjdk-headless
ENV KAFKA_VERSION="0.10.1.0" SCALA_VERSION="2.11"
RUN curl  http://apache.crihan.fr/dist/kafka/0.10.1.0/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz | tar -xzf - -C /opt/
ENV KAFKA_HOME /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}
COPY entrypoint /sbin/entrypoint
ADD  server.properties.jinja2 /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}/config/server.properties.jinja2
