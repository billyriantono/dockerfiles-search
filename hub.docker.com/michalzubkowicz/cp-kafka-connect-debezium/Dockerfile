FROM confluentinc/cp-kafka-connect:5.2.1

#WORKDIR /usr/local/
RUN wget http://client.hub.confluent.io/confluent-hub-client-latest.tar.gz
RUN mkdir confluent-hub-client-latest
RUN tar -xzf confluent-hub-client-latest.tar.gz -C confluent-hub-client-latest
RUN confluent-hub-client-latest/bin/confluent-hub install --no-prompt debezium/debezium-connector-mysql:0.9.4
RUN rm -Rf confluent-hub-client-latest/
