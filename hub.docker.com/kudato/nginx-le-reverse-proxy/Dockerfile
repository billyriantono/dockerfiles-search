FROM debian:stretch
MAINTAINER Alexander Shevchenko <kudato@me.com>

ENV DEBIAN_FRONTEND noninteractive
ENV TZ Europe/Moscow

ENV FQDN example.com
ENV EMAIL mail@example.com
ENV LETSENCRYPT true

ENV DESTINATION localhost

ENV HTTP 80
ENV HTTPS 443

ADD /config /templates_config
ADD /script/*.sh /
RUN chmod +x /*.sh && \
	ln -sf /healthcheck.sh /usr/bin/healthcheck && \
	ln -sf /magic.sh /usr/bin/magic
RUN magic setup

HEALTHCHECK --retries=3 --interval=15s --timeout=5s CMD healthcheck
ENTRYPOINT ["magic"]
CMD ["run"]




