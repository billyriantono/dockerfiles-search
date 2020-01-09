ARG ALPINE_VERSION=:3.9.2
FROM alpine$ALPINE_VERSION


LABEL maintainer="Caerm a.k.a Tomasz Czarnecki"


#!!!!!!!!!!!!!!!!!!!!!!
#!!! Install s6-overlay
ARG S6_OVERLAY_VERSION=v1.22.0.0
RUN apk add --no-cache --update curl \
    && curl -L -s https://github.com/just-containers/s6-overlay/releases/download/$S6_OVERLAY_VERSION/s6-overlay-amd64.tar.gz \
    | tar xvzf - -C / \
    && apk del --no-cache curl
#!!! Install s6-overlay
#!!!!!!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
#!!! Install duplicity and gnupg
ARG DUPLICITY_VERSION==0.7.18.2-r0
ARG GNUPG_VERSION==2.2.12-r0 
RUN apk add --no-cache --update \
    duplicity$DUPLICITY_VERSION \
    gnupg$GNUPG_VERSION
#!!! Install duplicity and gnupg
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
#!!! Create & populate config directory
RUN mkdir /statefull \
    && mkdir /statefull/gpg-keys \
    && mkdir /statefull/crontabs \
      && rm -r /etc/crontabs \
      && ln -s /statefull/crontabs /etc/crontabs
#!!! Create & populate config directory
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


ARG DOCKER_USER
ENV DOCKER_USER=${DOCKER_USER:-root}
ARG DOCKER_UID
ENV DOCKER_UID=${DOCKER_UID:-0}


#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
#!!! Every run initialization tasks
ARG INIT_TASK=00-add-user
RUN echo -e "#!/usr/bin/with-contenv /bin/sh\n\
\n\
cat /etc/passwd | grep -q \$DOCKER_USER\n\
if [ \$? -ne 0 ]; then\n\
  adduser -D -u \$DOCKER_UID \$DOCKER_USER\n\
  adduser \$DOCKER_USER tty\n\
fi\n\
" > /etc/cont-init.d/$INIT_TASK \
    && chmod +x /etc/cont-init.d/$INIT_TASK

ARG INIT_TASK=10-fix-crontabs
#Owner must be root
#Group with write to still edit that file, with that cron it works
RUN echo -e "#!/usr/bin/with-contenv /bin/sh\n\
\n\
if [ -e /statefull/crontabs/\$DOCKER_USER ]; then\n\
  chown root:\$DOCKER_USER /statefull/crontabs/\$DOCKER_USER\n\
  chmod 664 /statefull/crontabs/\$DOCKER_USER\n\
fi\n\
" > /etc/cont-init.d/$INIT_TASK \
    && chmod +x /etc/cont-init.d/$INIT_TASK

ARG INIT_TASK=20-gpg-keys-import
RUN echo -e "#!/usr/bin/with-contenv /bin/sh\n\
\n\
su - \$DOCKER_USER -c \"gpg --import /statefull/gpg-keys/*.pub\"\n\
su - \$DOCKER_USER -c \"gpg --import-ownertrust /statefull/gpg-keys/*.ownertrust\"\n\
" > /etc/cont-init.d/$INIT_TASK \
    && chmod +x /etc/cont-init.d/$INIT_TASK
#!!! Every run initialization tasks
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!!!!!!!!!
#!!! GPG key export-import
# To generate keys:
#   gpg --full-generate-key
# To list public and private keys:
#   gpg --list-keys
#   gpg --list-secret-keys
# To show/export specified pubkeys:
#   gpg --armor --export <fingerprint>  > <fingerprint>.pub
#   gpg --armor --export-secret-key <fingerprint>  > <fingerprint>.key
# To show/export ownertrusts:
#   gpg --export-ownertrust
#  and save line with selected fingerprint as <fingerprint>.ownertrust
# Importing:
#   gpg --import <file>
#   gpg --import-ownertrust <file>
#!!! GPG key export-import
#!!!!!!!!!!!!!!!!!!!!!!!!!


#!!!!!!!!!!!!!!!!!!!!!!
#!!! Create s6 services
ARG SERVICE_NAME=crond
RUN mkdir /etc/services.d/$SERVICE_NAME \
    && echo -e "#!/usr/bin/execlineb -P\n\
crond -f -L /dev/stdout" > /etc/services.d/$SERVICE_NAME/run \
    && chmod +x /etc/services.d/$SERVICE_NAME/run
#!!! Create s6 services
#!!!!!!!!!!!!!!!!!!!!!!


ENTRYPOINT ["/init"]

CMD []
