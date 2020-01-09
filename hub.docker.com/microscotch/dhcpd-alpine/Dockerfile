FROM alpine:3.9

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/microscotch/docker-dhcpd"
          
RUN apk update \
 && apk add dhcp dhcp-doc perl dumb-init mdocml

COPY util/entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
