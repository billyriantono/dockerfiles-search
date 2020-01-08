FROM debian:8

LABEL MAINTAINER "Ryar Nyah <ryarnyah@gmail.com>"

ENV IRCD_SERVER_NAME ircd.localhost
ENV IRCD_LOCATION ""

RUN apt-get update && \
    apt-get install -y \
            ircd-irc2 && \
    apt-get autoremove --purge -y && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 6667

CMD [ "/usr/sbin/ircd", "-t" ]
