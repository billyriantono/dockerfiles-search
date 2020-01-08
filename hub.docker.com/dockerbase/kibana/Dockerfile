# VERSION 1.1
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Kibana Image Container

FROM dockerbase/elasticsearch


# Run dockerbase script
ADD     kibana.sh /dockerbase/
RUN     /dockerbase/kibana.sh

ENV     KIBANA_HOME /usr/local/kibana
ENV     PATH $PATH:$KIBANA_HOME/bin

# Add kibana into runit
ADD     build/runit/kibana /etc/service/kibana/run

EXPOSE  5601
