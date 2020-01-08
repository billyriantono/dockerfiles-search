FROM confluentinc/cp-kafka-connect-base:5.2.1

RUN confluent-hub install --no-prompt confluentinc/kafka-connect-elasticsearch:5.2.0 \
    && confluent-hub install --no-prompt hpgrahsl/kafka-connect-mongodb:1.3.1
