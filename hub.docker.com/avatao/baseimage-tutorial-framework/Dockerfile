FROM avatao/frontend-tutorial-framework:chausie-20190915 as frontend
FROM avatao/debian:buster

RUN apt-get update                           &&\
    apt-get install -y --no-install-recommends \
        supervisor                             \
        libzmq5                                \
        nginx                                  \
        jq                                     \
        gettext-base                         &&\
    rm -rf /var/lib/apt/lists/*              &&\
    ln -sf /bin/bash /bin/sh

COPY requirements.txt /tmp
RUN pip3 install -r /tmp/requirements.txt

RUN curl -Ls https://github.com/krallin/tini/releases/download/v0.18.0/tini-amd64 --output /bin/init &&\
    echo "12d20136605531b09a2c2dac02ccee85e1b874eb322ef6baf7561cd93f93c855 /bin/init"                 |\
    sha256sum --check --status                                                                       &&\
    chmod 755 /bin/init

ENV TFW_PUBLIC_PORT=8888          \
    TFW_WEB_PORT=4242             \
    TFW_LOGIN_APP_PORT=6666       \
    TFW_TERMINADO_PORT=7878       \
    TFW_SUPERVISOR_HTTP_PORT=9001 \
    TFW_PUB_PORT=7654             \
    TFW_PULL_PORT=8765

EXPOSE ${TFW_PUBLIC_PORT}

ENV PYTHONPATH="/usr/local/lib"                                            \
    TFW_SUPERVISOR_HTTP_URI="http://localhost:${TFW_SUPERVISOR_HTTP_PORT}" \
    TFW_SUPERVISORD_CONF="/etc/supervisor/supervisord.conf"                \
    TFW_SUPERVISORD_COMPONENTS="/etc/supervisor/conf"                      \
    TFW_NGINX_CONF="/etc/nginx/nginx.conf"                                 \
    TFW_NGINX_DEFAULT="/etc/nginx/sites-enabled/default"                   \
    TFW_NGINX_COMPONENTS="/etc/nginx/components"                           \
    TFW_LIB_DIR="/usr/local/lib"                                           \
    TFW_FRONTEND_DIR="/srv/frontend"                                       \
    TFW_DIR="/.tfw"                                                        \
    TFW_SERVER_DIR="/.tfw/tfw_server"                                      \
    TFW_AUTH_KEY="/tmp/tfw-auth.key"                                       \
    TFW_LOGS_DIR="/var/log/tfw"                                            \
    TFW_PIPES_DIR="/run/tfw"                                               \
    TFW_SNAPSHOTS_DIR="/tmp/tfw-snapshots"                                 \
    TFW_HISTFILE="/home/${AVATAO_USER}/.bash_history"                      \
    PROMPT_COMMAND="history -a"

COPY bashrc supervisor/tfw_init.sh /tmp/
COPY supervisor/supervisord.conf ${TFW_SUPERVISORD_CONF}
COPY supervisor/components/ ${TFW_SUPERVISORD_COMPONENTS}
COPY nginx/nginx.conf ${TFW_NGINX_CONF}
COPY nginx/default.conf ${TFW_NGINX_DEFAULT}
COPY nginx/components/ ${TFW_NGINX_COMPONENTS}
COPY tfw ${TFW_LIB_DIR}/tfw
COPY supervisor/tfw_server.py ${TFW_SERVER_DIR}/
COPY --from=frontend /srv/dist ${TFW_FRONTEND_DIR}

VOLUME ["${TFW_LOGS_DIR}", "${TFW_PIPES_DIR}"]

ONBUILD ARG BUILD_CONTEXT="solvable"

ONBUILD COPY ${BUILD_CONTEXT}/nginx/ ${TFW_NGINX_COMPONENTS}
ONBUILD COPY ${BUILD_CONTEXT}/supervisor/ ${TFW_SUPERVISORD_COMPONENTS}

ONBUILD RUN for f in "${TFW_NGINX_DEFAULT}" ${TFW_NGINX_COMPONENTS}/*.conf; do                               \
                envsubst "$(printenv | cut -d= -f1 | grep TFW_ | sed -e 's/^/$/g')" < $f > $f~ && mv $f~ $f ;\
            done
ONBUILD VOLUME ["/etc/nginx", "/var/lib/nginx", "/var/log/nginx", "${TFW_LIB_DIR}/tfw"]

ENTRYPOINT ["/bin/init", "--"]
CMD exec supervisord --nodaemon --configuration ${TFW_SUPERVISORD_CONF}
