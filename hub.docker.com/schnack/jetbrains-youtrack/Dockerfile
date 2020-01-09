FROM            debian:jessie

MAINTAINER      "Mikhail Stolyarov" <schnack.desu@gmail.com>

#ARG            port=8080 

ENV             APP_VERSION=6.5 \
                APP_BUILD=17057 \
                APP_USER=youtrack \
                APP_STATIC_DIR=/opt/youtrack \
                APP_DYNAMIC_DIR=/var/opt/youtrack \
                APP_LISTEN_PORT=${port:-8080}

LABEL           description="YouTrack introduces a number of integrations, simplified Jira import, redesigned Administration UI, and many other important enhancements." \
                version=$APP_VERSION \
                build=$APP_BUILD \
                url="https://www.jetbrains.com/youtrack/"
	
RUN             apt-get update \
                && apt-get install -y unzip \
                && apt-get install -y wget \
                && mkdir -p $APP_STATIC_DIR \
                && mkdir -p $APP_DYNAMIC_DIR \
                && useradd -m -d $APP_DYNAMIC_DIR -s /usr/sbin/nologin -c "JetBrains" -U $APP_USER \
                && wget -q -P /tmp https://download.jetbrains.com/charisma/youtrack-${APP_VERSION}.${APP_BUILD}.zip \
                && unzip /tmp/youtrack-${APP_VERSION}.${APP_BUILD}.zip -d $APP_STATIC_DIR \
                && apt-get purge -y unzip \
                && apt-get purge -y wget \
                && apt-get autoclean \
                && apt-get clean \
                && rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/* \
                && ${APP_STATIC_DIR}/bin/youtrack.sh configure \
                        --backups-dir=${APP_DYNAMIC_DIR}/backups \
                        --temp-dir=${APP_DYNAMIC_DIR}/temp \
                        --data-dir=${APP_DYNAMIC_DIR}/data \
                        --logs-dir=${APP_DYNAMIC_DIR}/logs \
                        --listen-port=$APP_LISTEN_PORT \ 
                && chown -R ${APP_USER}:${APP_USER} $APP_STATIC_DIR \
                && chown -R ${APP_USER}:${APP_USER} $APP_DYNAMIC_DIR 

USER            $APP_USER

WORKDIR         $APP_STATIC_DIR

EXPOSE          $APP_LISTEN_PORT

VOLUME          ["$APP_DYNAMIC_DIR","$APP_STATIC_DIR/conf"]

ENTRYPOINT      ["bin/youtrack.sh"]

CMD             ["run"]
