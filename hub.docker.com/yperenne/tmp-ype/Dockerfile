ARG version=latest
FROM ubuntu:$version
#MAINTAINER JCD "jcd717@outlook.com"
LABEL maintainer="maintainer: JCD <jcd717@outlook.com>" \
      desciption="test" \
      auteur="bruno dubois" 

COPY heartbeat.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ARG hbs=4
ENV HEARTBEATSTEP $hbs
EXPOSE 1234/udp 4321/tcp

ENTRYPOINT ["/entrypoint.sh"]
CMD ["battement"]

