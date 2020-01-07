FROM golang:1.8.3-jessie
 
RUN curl http://packages.confluent.io/deb/3.3/archive.key | apt-key add - &&\
    echo "deb [arch=amd64] http://packages.confluent.io/deb/3.3 stable main" >> /etc/apt/sources.list && \
    apt-get update && apt-get install -y librdkafka-dev

# preload and cache dependencies
RUN go get github.com/confluentinc/confluent-kafka-go/kafka