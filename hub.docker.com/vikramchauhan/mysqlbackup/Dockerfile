FROM vikramchauhan/mysqlcli:debian as mysqlcli

ENV MYSQLCLI_DIR=/mysqlcli

RUN mkdir $MYSQLCLI_DIR \
    && mkdir $MYSQLCLI_DIR/lib \
    && cp -fv /usr/bin/mysql* $MYSQLCLI_DIR \
    && ldd /usr/bin/mysql | cut -d ' ' -f 3 | xargs -Isrc cp src $MYSQLCLI_DIR/lib

FROM python:3-slim
MAINTAINER Vikram Chauhan <me@vkrm.ch>

ARG RUN_USER=coco
ARG RUN_GROUP=coco
ARG RUN_UID=5555
ARG RUN_GID=5555
ARG RUN_PASS=coco123@
ARG DEPS="ca-certificates \
        wget \
        unzip \
        git"
ARG MYSQLCLI_DIR=/mysqlcli
ARG MYSQLCLI_OUTPUT_DIR=/output
ARG APP_CFG_DIR=/config

ENV RUN_USER=${RUN_USER} \
    RUN_GROUP=${RUN_GROUP} \
    RUN_UID=${RUN_UID} \
    RUN_GID=${RUN_GID} \
    LD_LIBRARY_PATH="$MYSQLCLI_DIR/lib" \
    PATH="$MYSQLCLI_DIR:$LD_LIBRARY_PATH:$PATH"

COPY --from=mysqlcli $MYSQLCLI_DIR $MYSQLCLI_DIR

RUN groupadd -g $RUN_GID $RUN_GROUP \
    && useradd -m $RUN_USER -c "Run Account" -g $RUN_GROUP -u $RUN_UID -p $RUN_PASS \
    && chown -R $RUN_USER:$RUN_GROUP $MYSQLCLI_DIR \
    && chmod -R 755 $MYSQLCLI_DIR \
    && apt-get -y update \
    && apt-get -y install --no-install-recommends ${DEPS} \
    && cd / \
    && wget https://github.com/vikc07/mysqlbackup/archive/master.zip \
    && unzip master.zip \
    && mv mysqlbackup-master app \
    && rm master.zip \
    && rm -rf /var/lib/apt/lists/* \
    && pip install -r app/requirements.txt \
    && mkdir $APP_CFG_DIR \
    && cp /app/mysqlbackup/cfg/sample_mysqlbackup.json $APP_CFG_DIR/mysqlbackup.json \
    && mv /app/mysqlbackup/cfg /app/mysqlbackup/cfg_orig \
    && ln -s /config /app/mysqlbackup/cfg \
    && mkdir $MYSQLCLI_OUTPUT_DIR \
    && chown -R $RUN_USER:$RUN_GROUP /app \
    && chown -R $RUN_USER:$RUN_GROUP $APP_CFG_DIR \
    && chown -R $RUN_USER:$RUN_GROUP $MYSQLCLI_OUTPUT_DIR \
    && apt-get -y remove ${DEPS} \
    && apt-get -y clean \
    && apt-get -y autoclean \
    && apt-get -y autoremove

USER $RUN_USER

# Set entrypoint
ENTRYPOINT ["sh","-c"]