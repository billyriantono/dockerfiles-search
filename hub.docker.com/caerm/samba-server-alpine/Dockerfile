ARG ALPINE_VERSION=:3.9.2
FROM alpine$ALPINE_VERSION


LABEL maintainer="Caerm"


#!!!!!!!!!!!!!!!!!!!!!!
#!!! Install s6-overlay
ARG S6_OVERLAY_VERSION=v1.22.0.0
RUN apk add --no-cache --update curl \
    && curl -L -s https://github.com/just-containers/s6-overlay/releases/download/$S6_OVERLAY_VERSION/s6-overlay-amd64.tar.gz \
    | tar xvzf - -C / \
    && apk del --no-cache curl
#!!! Install s6-overlay
#!!!!!!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!
#!!! Install samba
ARG SAMBA_VERSION==4.8.8-r0
RUN apk add --no-cache --update \
    samba-common-tools$SAMBA_VERSION \
#    samba-client$SAMBA_VERSION \
    samba-server$SAMBA_VERSION
#!!! Install samba
#!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
#!!! Create & populate config directory
RUN mkdir /statefull \
    && touch /statefull/check_file
#!!! Create & populate config directory
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
#!!! Every run initialization tasks
ARG INIT_TASK=00-statefull-prepare
RUN echo -e "#!/bin/sh\n\
if [ ! -e /statefull/check_file ]; then\n\
  mkdir /statefull/etc/\n\
  mv /etc/passwd /statefull/etc/\n\
  mv /etc/shadow /statefull/etc/\n\
  mv /etc/group /statefull/etc/\n\
  ln -s /statefull/etc/* /etc/\n\
  mv /etc/samba /statefull/etc\n\
  ln -s /statefull/etc/samba /etc\n\
  mkdir -p /statefull/var/lib/samba/\n\
  mv /var/lib/samba/private/ /statefull/var/lib/samba/\n\
  ln -s /statefull/var/lib/samba/private /var/lib/samba/\n\
  touch /statefull/check_file\n\
fi\n\
" > /etc/cont-init.d/$INIT_TASK \
    && chmod +x /etc/cont-init.d/$INIT_TASK
#!!! Every run initialization tasks
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!!!!!!
#!!! Create s6 services
ARG SERVICE_NAME=smbd
RUN mkdir /etc/services.d/$SERVICE_NAME \
    && echo -e "#!/usr/bin/execlineb -P\n\
smbd --foreground --no-process-group --log-stdout" > /etc/services.d/$SERVICE_NAME/run \
    && chmod +x /etc/services.d/$SERVICE_NAME/run
#!!! Create s6 services
#!!!!!!!!!!!!!!!!!!!!!!


EXPOSE 445/tcp

ENTRYPOINT ["/init"]

CMD []
