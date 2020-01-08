FROM java:8

COPY . /kafka-manager
WORKDIR /kafka-manager
RUN ./sbt clean dist
EXPOSE 9000
ENV ZK_HOSTS localhost:2181
CMD ["bin/kafka-manager"]
