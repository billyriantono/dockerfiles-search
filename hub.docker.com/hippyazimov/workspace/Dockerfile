FROM stunteam/alpine:node

ARG SUPERVISOR_USER=supervisor
ARG SUPERVISOR_PASSWORD=supervisor
ARG APP_GROUP_UID=1000
ARG APP_GROUP_NAME=app
ARG APP_USER_UID=1000
ARG APP_USER_NAME=app
ARG APP_USER_PASSWORD=app
ARG APP_HOME_DIR=/app
ARG FIREFOX_VERSION=61.0
ARG IDEA_VERSION=2018.1.5
ARG ROOT_PASSWORD=1
ARG APP_USER_SHELL=/bin/sh
ARG GLIBC_PACKAGE_VERSION=2.27-r0

ENV SUPERVISOR_USER=${SUPERVISOR_USER}
ENV SUPERVISOR_PASSWORD=${SUPERVISOR_PASSWORD}
ENV APP_GROUP_UID=${APP_GROUP_UID}
ENV APP_GROUP_NAME=${APP_GROUP_NAME}
ENV APP_USER_UID=${APP_USER_UID}
ENV APP_USER_NAME=${APP_USER_NAME}
ENV APP_HOME_DIR=${APP_HOME_DIR}
ENV APP_USER_PASSWORD=${APP_USER_PASSWORD}
ENV FIREFOX_VERSION=${FIREFOX_VERSION}
ENV IDEA_VERSION=${IDEA_VERSION}
ENV ROOT_PASSWORD=${ROOT_PASSWORD}
ENV APP_USER_SHELL=${APP_USER_SHELL}
ENV GLIBC_PACKAGE_VERSION=${GLIBC_PACKAGE_VERSION}
ENV LANG=C.UTF-8

COPY config/etc/apk/repositories /etc/apk/repositories

#>>> Supervisor
COPY config/etc/supervisor.d/ /etc/supervisor.d/
COPY config/packages/supervisor.sh /var/build-scripts/supervisor.sh
RUN /bin/sh /var/build-scripts/supervisor.sh
EXPOSE 9001
#<<< Supervisor

#>>> Xorg RDP
COPY config/etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini
COPY config/etc/xrdp/startwm.sh /etc/xrdp/startwm.sh
COPY config/packages/xrdp.sh /var/build-scripts/xrdp.sh
RUN /bin/sh /var/build-scripts/xrdp.sh
EXPOSE 3389
#<<< Xorg RDP

#>>> Firefox
COPY config/packages/firefox.sh /var/build-scripts/firefox.sh
RUN /bin/sh /var/build-scripts/firefox.sh
#<<< Firefox

#>>> NodeJS dependencies
COPY config/packages/nodejs-dependencies.sh /var/build-scripts/nodejs-dependencies.sh
RUN /bin/sh /var/build-scripts/nodejs-dependencies.sh
#<<< NodeJS dependencies

#>>> Qtile
COPY config/packages/qtile.sh /var/build-scripts/qtile.sh
RUN /bin/sh /var/build-scripts/qtile.sh
#<<< Qtile

#>>> Sudo
COPY config/packages/sudo.sh /var/build-scripts/sudo.sh
RUN /bin/sh /var/build-scripts/sudo.sh
#<<< Sudo

#>>> Glibc
COPY config/packages/glibc.sh /var/build-scripts/glibc.sh
RUN /bin/sh /var/build-scripts/glibc.sh
#<<< Glibc

#>>> Intellij Idea
ENV JAVA_HOME=/usr/lib/jvm/default-jvm/
COPY config/packages/idea.sh /var/build-scripts/idea.sh
RUN /bin/sh /var/build-scripts/idea.sh
#<<< Intellij Idea

COPY config/entrypoint.sh /var/entrypoint.sh
ENTRYPOINT /bin/sh /var/entrypoint.sh

