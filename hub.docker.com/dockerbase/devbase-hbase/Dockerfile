# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Devbase-hbase Image Container

FROM dockerbase/devbase-jdk

USER    root

# Run dockerbase script
ADD     hbase.sh /dockerbase/
RUN     /dockerbase/hbase.sh

ENV     HBASE_HOME /usr/local/hbase
ENV     PATH $PATH:$HBASE_HOME/bin

# Add configuration into hbase
ADD     build/conf/hbase-site.xml /usr/local/hbase/conf/hbase-site.xml

USER    devbase

# Set environment variables.
ENV     HOME /home/devbase

# Define working directory.
WORKDIR /home/devbase

