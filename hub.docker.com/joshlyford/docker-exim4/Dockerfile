FROM debian:jessie

MAINTAINER Josh Lyford "joshlyford@gmail.com"

RUN apt-get update && \
    apt-get install -y exim4-daemon-heavy && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    find /var/log -type f | while read f; do echo -ne '' > $f; done;

RUN apt-get update && apt-get install -y \
        nano \
        wget \
        git 

COPY 00_local_macros /etc/exim4/conf.d/main/
COPY entrypoint.sh /bin/

RUN chmod a+x /bin/entrypoint.sh

ENV TERM xterm

EXPOSE 25
ENTRYPOINT ["/bin/entrypoint.sh"]
CMD ["exim", "-bd", "-q15m", "-v"]
