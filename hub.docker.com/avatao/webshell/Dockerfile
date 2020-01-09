FROM avatao/ubuntu:16.04

# install some dependencies
RUN apt-get update &&\
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - &&\
    apt-get install -qy supervisor nodejs

# configure environment
ENV TFW_WORKDIR="/home/user/challenge" \
    TFW_WSHELLDIR="/srv/.webshell" \
    TFW_SUPERVISORD_CONF="/etc/supervisor/supervisord.conf"

# set up webshell
COPY ./src/webshell ${TFW_WSHELLDIR}
RUN mkdir ${TFW_WORKDIR} &&\
    npm install --prefix ${TFW_WSHELLDIR}

# set up supervisord
ENV TFW_SUPERVISORD_CONFIGDIR="/etc/supervisor/conf"
COPY ./src/supervisord.conf ${TFW_SUPERVISORD_CONF}
RUN chown -R ${AVATAO_USER}: ${TFW_WORKDIR} &&\
    mkdir ${TFW_SUPERVISORD_CONFIGDIR} &&\
    sed -i "s#{{TFW_WSHELLDIR}}#${TFW_WSHELLDIR}#g" ${TFW_SUPERVISORD_CONF} &&\
    sed -i "s#{{TFW_SUPERVISORD_CONFIGDIR}}#${TFW_SUPERVISORD_CONFIGDIR}#g" ${TFW_SUPERVISORD_CONF}

WORKDIR ${TFW_WORKDIR}
VOLUME ["${TFW_WORKDIR}"]
CMD exec supervisord --nodaemon
