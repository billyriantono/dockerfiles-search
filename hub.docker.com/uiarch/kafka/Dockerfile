FROM uiarch/jre:8

MAINTAINER Kyle K. Lin <gazer.kanlin@gmail.com>

# Create user
RUN adduser kafka -m

RUN set -x \
    && cd /opt \
    && curl http://ftp.twaren.net/Unix/Web/apache/kafka/0.11.0.0/kafka_2.11-0.11.0.0.tgz > kafka_2.11-0.11.0.0.tgz \
    && tar -xzvf kafka_2.11-0.11.0.0.tgz \
    && rm kafka_2.11-0.11.0.0.tgz

COPY server.properties /opt/kafka_2.11-0.11.0.0/config
    
RUN set -x \
    && mkdir /opt/kafka_2.11-0.11.0.0/logs \
    && chown -R kafka:kafka /opt/kafka_2.11-0.11.0.0

# Setup PATH
ENV PATH /opt/kafka_2.11-0.11.0.0/bin:$PATH

# Setup working directory
WORKDIR /opt/kafka_2.11-0.11.0.0

# Switch user
USER kafka

# Expose ports
EXPOSE 9160

# Run
CMD ["/bin/bash"]
