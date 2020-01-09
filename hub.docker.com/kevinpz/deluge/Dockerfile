FROM fedora
MAINTAINER Kevin Printz

RUN dnf install -y deluge-web && \
    dnf clean all

RUN dnf install -y supervisor

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

VOLUME ["/config","/data"] 

EXPOSE 8112

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
