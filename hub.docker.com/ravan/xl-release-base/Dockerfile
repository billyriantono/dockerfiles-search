ARG XLR_BASE=xebialabs/xl-release:9.0.6
FROM $XLR_BASE as source

FROM groovy:2.5.8-jdk8 AS builder
USER root
ENV APP_ROOT=/opt/xebialabs APP_HOME=/opt/xebialabs/xl-release-server
WORKDIR $APP_ROOT
COPY --from=source $APP_HOME $APP_HOME
COPY --from=source $APP_ROOT/db-libs dblibs
COPY --from=source ${APP_ROOT}/tini ${APP_HOME}/bin/tini
COPY resources/reset.groovy reset.groovy
RUN chmod ugo+x ${APP_HOME}/bin/tini && \
    groovy reset.groovy

FROM openjdk:8-alpine
LABEL maintainer="rnaidoo@xebialabs.com"
ENV USER_ID=xebialabs \
    APP_ROOT=/opt/xebialabs \
    APP_HOME=/opt/xebialabs/xl-release-server \
    GROOVY_HOME=/opt/groovy
COPY --from=builder ${APP_HOME} ${APP_HOME}
COPY --from=builder ${GROOVY_HOME} ${GROOVY_HOME}
RUN apk --no-cache add curl && \
    ln -s "${GROOVY_HOME}/bin/groovy" /usr/bin/groovy && \
    addgroup -S ${USER_ID} && adduser -S -G ${USER_ID} ${USER_ID}
WORKDIR ${APP_HOME}
EXPOSE 5516
ENTRYPOINT []
CMD ["/opt/xebialabs/xl-release-server/bin/tini", "--", "/opt/xebialabs/xl-release-server/bin/run.sh"]

