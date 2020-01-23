FROM gcr.io/google_containers/ubuntu-slim:0.4
MAINTAINER Abderraouf BEN SALEM "abderraouf.bensalem@ricardo.ch"

# Ensure there are enough file descriptors for running Fluentd.
RUN ulimit -n 65536

# Disable prompts from apt.
ENV DEBIAN_FRONTEND noninteractive

# Install fluentd
COPY install.sh /tmp/install.sh
RUN sh /tmp/install.sh

# Copy the Fluentd configuration file.
COPY td-agent.conf /etc/td-agent/td-agent.conf

ENV ELASTICSEARCH_PORT 9200

# Run the Fluentd service.
ENTRYPOINT ["td-agent"]

EXPOSE 24284
