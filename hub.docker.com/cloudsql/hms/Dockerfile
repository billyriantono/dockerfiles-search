FROM java:7

# Dockerize
ENV DOCKERIZE_VERSION v0.2.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Hive Metastore Service
ENV HIVE_HOME=/opt/hive \
    HIVE_VERSION=1.2.1 \
    METASTORE_PORT=9083

RUN mkdir -p $HIVE_HOME  %HIVE_HOME/conf
WORKDIR $HIVE_HOME

# COPY hms-all.tar.gz $HIVE_HOME/
RUN set -x \
    && wget https://shzhaowu.blob.core.windows.net/prestohms/hms-all.tar.gz \
    && tar -xvf hms-all.tar.gz \
    && rm hms-all.tar.gz*

COPY templates/log4j.properties.tmpl $HIVE_HOME/conf/
COPY templates/hive-site.xml.tmpl $HIVE_HOME/conf/

COPY hms_launcher.sh $HIVE_HOME/launcher
RUN chmod +x $HIVE_HOME/launcher

CMD $HIVE_HOME/launcher
