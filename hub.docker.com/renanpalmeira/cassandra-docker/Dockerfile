# renanpalmeira/cassandra
#
# VERSION               0.1

FROM dockerfile/java:oracle-java7
MAINTAINER Renan Palmeira <renan@forleven.com>

ENV DEBIAN_FRONTEND noninteractive
ENV INITRD No

# Add DataStax sources
ADD datastax_key /tmp/datastax_key
RUN apt-key add /tmp/datastax_key
RUN echo "deb http://debian.datastax.com/community stable main" > /etc/apt/sources.list.d/datastax.list

# Install Cassandra 2.0.13
RUN apt-get update && \
    apt-get install -y default-jdk cassandra=2.0.13 dsc20=2.0.13-1 && \
    rm -rf /var/lib/apt/lists/*

ENV CASSANDRA_CONFIG /etc/cassandra

RUN /usr/local/bin/config-cassandra-base
RUN rm -f /etc/security/limits.d/cassandra.conf

EXPOSE 7199 7000 7001 9160 9042 22 8012 61621

CMD [""]