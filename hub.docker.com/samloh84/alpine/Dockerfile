FROM alpine:3.6

ARG APP_UID=1000
ARG APP_GID=1000
ARG APP_USERNAME=appuser
ARG APP_GROUPNAME=appuser
ARG APP_USER_HOME=/usr/src/app

ENV ROOT_UID 0
ENV APP_UID ${APP_UID}
ENV APP_GID ${APP_GID}
ENV APP_USERNAME ${APP_USERNAME}
ENV APP_GROUPNAME ${APP_GROUPNAME}
ENV APP_USER_HOME ${APP_USER_HOME}
ENV HOME ${APP_USER_HOME}

USER ${ROOT_UID}

COPY fix-permissions fix-ownership apk-install /usr/local/bin/

RUN chmod a+rxs /usr/local/bin/fix-permissions \
/usr/local/bin/fix-ownership \
/usr/local/bin/apk-install && \
apk-install shadow coreutils git nano curl openssl && \
mkdir -p `dirname ${APP_USER_HOME}` && \
groupadd --gid ${APP_GID} ${APP_GROUPNAME} && \
useradd --uid ${APP_UID} --gid ${APP_GID} \
--create-home \
--home-dir ${APP_USER_HOME} \
--shell /sbin/nologin \
--comment "App User" \
${APP_USERNAME}

USER ${APP_UID}

WORKDIR ${APP_USER_HOME}

CMD /bin/ash
