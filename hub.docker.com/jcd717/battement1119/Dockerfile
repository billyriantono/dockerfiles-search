
ARG version=latest
FROM ubuntu:$version

#MAINTAINER JCD "jcd717@outlook.com"

LABEL maintainer="JCD <jcd717@outlook.com>" \
      description="test" \
      auteur="bruno dubois"  \
      clef="valeur"

COPY heartbeat.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh && \
    echo coucou >test.txt

ARG hbs=2
ENV HEARTBEATSTEP $hbs


# information de port réseau utile
EXPOSE 1234/udp 4321/tcp

WORKDIR /bin

ENTRYPOINT ["/entrypoint.sh"]
CMD ["battement"]

# ARG msg=battement
# ENV msg $msg
# CMD ["/entrypoint.sh","$msg"]
