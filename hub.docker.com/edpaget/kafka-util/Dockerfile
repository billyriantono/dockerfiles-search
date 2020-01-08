# DOCKER-VERSION 1.2.0
# VERSION 0.3

FROM zooniverse/kafka
MAINTAINER Edward Paget <ed@zooniverse.org>

RUN echo "#!/bin/bash \n./opt/kafka_$SCALA_VERSION-$KAFKA_VERSION/bin/kafka-console-consumer.sh \$@" > /usr/local/bin/kafka-consumer && \
    chmod +x /usr/local/bin/kafka-consumer

ENTRYPOINT ["kafka-consumer"]
