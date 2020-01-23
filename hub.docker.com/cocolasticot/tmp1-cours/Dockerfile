ARG version=latest
FROM ubuntu:$version
MAINTAINER JCD "jcd717@outlook.com"

LABEL  maintainer="JCD jcd717@outlook.com" \
       description="test" \
       auteur="bruno dubois" 

#ARG hbs=2

COPY heartbeat.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh ; \
    echo cocolasticot >test.txt


ARG hbs=3
ENV HEARTBEATSTEP $hbs


#Information de port réseau utile
EXPOSE 1234



ENTRYPOINT ["/entrypoint.sh"]
CMD ["battement"]

