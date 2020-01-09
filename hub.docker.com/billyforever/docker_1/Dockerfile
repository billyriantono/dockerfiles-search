ARG version=latest
FROM ubuntu:${version}
MAINTAINER JCD "jcd717@outlook.com"



COPY heartbeat.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh ; \
    echo coucou > test.txt

ARG hbs=3
ENV HEARTBEATSTEP $hbs


ENTRYPOINT ["/entrypoint.sh"]
CMD ["Hello"]
