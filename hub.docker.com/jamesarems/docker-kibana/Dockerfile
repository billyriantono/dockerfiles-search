#Creating Images for Kibana Image 
FROM jamesarems/kibana:beta1
MAINTAINER James PS <jamesarems@gmail.com>

#Updating Ubuntu packages

COPY ./start.sh /usr/bin/
#RUN rm -rf /usr/
#COPY ./test.pl /usr/share
RUN chmod +x /usr/bin/start.sh

#Exposing tcp ports
EXPOSE 5601
#EXPOSE 125
#EXPOSE 25

#Adding volume
#VOLUME /usr/share/kibana
VOLUME /etc/kibana

#Running final script
ENTRYPOINT ["/usr/bin/start.sh"]
