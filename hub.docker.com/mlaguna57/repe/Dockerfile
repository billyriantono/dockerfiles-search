FROM ubuntu:latest  
LABEL maintainer="jp.gouigoux@free.es"  
COPY heartbeat.sh /entrypoint.sh  
RUN chmod +x /entrypoint.sh  
ENV HEARTBEATSTEP 1
ENTRYPOINT ["/entrypoint.sh"]
CMD ["heartbeat"]
