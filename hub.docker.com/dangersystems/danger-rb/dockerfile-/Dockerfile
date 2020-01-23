FROM ubuntu:14.04
MAINTAINER Daniel Hess <dan9186@gmail.com>

# Update and install deps
RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y wget

# Add RabbitMQ Repo
RUN echo "deb http://www.rabbitmq.com/debian/ testing main" >> /etc/apt/sources.list && \
    wget -qO - http://deb.opera.com/archive.key | sudo apt-key add -

# Install RabbitMQ
RUN apt-get install -y rabbitmq-server

# Clean up
RUN apt-get autoremove -y && \
    apt-get clean

# Configure RabbitMQ
RUN rabbitmq-plugins enable rabbitmq_management
ADD rabbitmq.config /etc/rabbitmq/rabbitmq.config

# Define environment variables.
ENV RABBITMQ_LOG_BASE /data/log
ENV RABBITMQ_MNESIA_BASE /data/mnesia

# Define mount points.
VOLUME ["/data/log", "/data/mnesia"]

EXPOSE 5672 15672

ADD docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
