FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive

# Install packages
ADD provision.sh /provision.sh
ADD serve.sh /serve.sh

ADD supervisor.conf /etc/supervisor/conf.d/supervisor.conf

RUN chmod +x /*.sh && \
    ./provision.sh

VOLUME /apps

EXPOSE 80
CMD ["/usr/bin/supervisord"]
