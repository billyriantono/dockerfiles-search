FROM alpine:edge

COPY configure.sh /
RUN /bin/sh /configure.sh

COPY init.sh /init.sh
COPY entrypoint.sh /entrypoint.sh
COPY templates /templates

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]

CMD ["/bin/sh", "/init.sh"]
