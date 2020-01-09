FROM java:jre-alpine
MAINTAINER "Michel Buczynski" michel@service-bmi.com
#Based on "Eugene Janusov" <esycat@gmail.com>

ENV APP_VERSION 6.5
ENV APP_BUILD ${APP_VERSION}.17057
ENV APP_PORT 8080
ENV APP_SUFFIX youtrack
ENV APP_UID 2000

ENV APP_DISTNAME youtrack-${APP_BUILD}
ENV APP_DISTFILE youtrack-2017.2.33766.zip
ENV APP_PREFIX /opt
ENV APP_DIR $APP_PREFIX/$APP_SUFFIX
ENV APP_HOME /var/lib/$APP_SUFFIX
# preparing home (data) directory and user+group
#we are with Alpine linux no /opt
RUN mkdir -p $APP_PREFIX
RUN mkdir -p $APP_DIR
RUN mkdir $APP_HOME

# downloading and unpacking the distribution, removing bundled JVMs
# direct link https://download.jetbrains.com/charisma/youtrack-6.5.17057.zip
WORKDIR $APP_PREFIX
RUN apk update && apk add wget 
#to switch from busybox to bash
#RUN apk add bash && ln -sf /bin/bash /bin/sh
RUN wget -q --no-check-certificate https://download.jetbrains.com/charisma/$APP_DISTFILE && \
    unzip -q $APP_DISTFILE -d $APP_DIR && \
    rm $APP_DISTFILE && \
    rm -rf $APP_DIR/internal/java
RUN ls $APP_DIR/youtrack-2017.2.33766 && ls $APP_DIR/youtrack-2017.2.33766/bin    
RUN apk del wget && rm /var/cache/apk/*

WORKDIR $APP_DIR

RUN /opt/youtrack/youtrack-2017.2.33766/bin/youtrack.sh configure \
    --backups-dir $APP_HOME/backups \
    --data-dir    $APP_HOME/data \
    --logs-dir    $APP_HOME/log \
    --temp-dir    $APP_HOME/tmp \
    --listen-port $APP_PORT \
    --base-url    http://localhost:$APP_PORT/

ENTRYPOINT ["/opt/youtrack/youtrack-2017.2.33766/bin/youtrack.sh"]
CMD ["run"]
EXPOSE $APP_PORT
VOLUME ["$APP_HOME"]
