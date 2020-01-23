FROM rancher/confd-base:0.11.0-dev-rancher

ADD ./conf.d /etc/confd/conf.d
ADD ./templates /etc/confd/templates

ENTRYPOINT ["/confd"]
CMD ["--backend", "rancher", "--prefix", "/latest", "--log-level", "debug"]
