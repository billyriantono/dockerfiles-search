FROM docker.elastic.co/kibana/kibana:5.6.15

MAINTAINER tomas.hejatko@gmail.com

COPY --chown=kibana:kibana kibana.yml /usr/share/kibana/config/
#COPY --chown=elasticsearch:elasticsearch config/log4j2.properties /usr/share/elasticsearch/config/

#RUN rm -Rf /usr/share/kibana/x-pack

#RUN rm -Rf /usr/share/kibana/modules/x-pack*

RUN rm -Rf /usr/share/kibana/plugins/x-pack*