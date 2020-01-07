# Spotify Cassandra 2.1 Base Image
#
# VERSION               0.2
#
# Installs Cassandra 2.1 package. Does only basic configuration.
# Tokens and seed nodes should be configured by child images.

FROM vovimayhem/java:oracle-java7

# Workaround for https://github.com/docker/docker/issues/6345
RUN ln -s -f /bin/true /usr/bin/chfn

# Set the cassandra version:
ENV CASSANDRA_VERSION 2.1.2

# Install curl, then cassandra, then remove curl:
RUN apt-get update \
&& apt-get install -y curl --no-install-recommends \
&& curl -L http://debian.datastax.com/debian/repo_key | apt-key add - \
&& echo "deb http://debian.datastax.com/community stable main" > /etc/apt/sources.list.d/datastax.list \
&& apt-get update \
&& apt-get install -y cassandra=$CASSANDRA_VERSION \
&& apt-get remove -y curl && apt-get -y autoremove \
&& rm -rf /var/lib/apt/lists/*

# Disable virtual nodes:
RUN sed -i -e "s/num_tokens/\# num_tokens/" /etc/cassandra/cassandra.yaml

# Set the Cassandra's configuration path
ENV CASSANDRA_CONFIG /etc/cassandra
VOLUME ["/etc/cassandra"]

# Necessary since cassandra is trying to override the system limitations
# See https://groups.google.com/forum/#!msg/docker-dev/8TM_jLGpRKU/dewIQhcs7oAJ
RUN rm -f /etc/security/limits.d/cassandra.conf

EXPOSE 7199 7000 7001 9160 9042 22 8012 61621
