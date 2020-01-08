FROM java:8

ENV UPSOURCE_VERSION 2.0.3554

RUN wget http://download.jetbrains.com/upsource/upsource-$UPSOURCE_VERSION.zip \
    && unzip upsource-$UPSOURCE_VERSION.zip -d /opt \
    && rm upsource-$UPSOURCE_VERSION.zip

VOLUME ["/opt/Upsource/conf", "/opt/Upsource/data", "/opt/Upsource/logs", "/opt/Upsource/backups"]

EXPOSE 8080

WORKDIR /opt/Upsource

ENTRYPOINT ["bin/upsource.sh", "run"]
