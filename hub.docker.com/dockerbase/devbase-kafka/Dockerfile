# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Devbase-kafka Image Container

FROM dockerbase/devbase-scala

USER    root

# Run dockerbase script
ADD     kafka.sh /dockerbase/
RUN     /dockerbase/kafka.sh

ENV     KAFKA_HOME /usr/local/kafka
ENV     PATH $PATH:$KAFKA_HOME/bin

USER    devbase

# Set environment variables.
ENV     HOME /home/devbase

# Define working directory.
WORKDIR /home/devbase

