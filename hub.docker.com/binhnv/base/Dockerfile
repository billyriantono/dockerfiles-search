FROM phusion/baseimage:0.11
LABEL maintainer="Binh Van Nguyen<binhnv80@gmail.com>"

ENV TERM="xterm" \
    MY_USER="myuser" \
    MY_INIT_DIR="/etc/my_init.d" \
    MY_SERVICE_DIR="/etc/service" \
    SERVICES_ENABLED_LIST="" \
    MY_APP_DIR="/usr/local" \
    MY_APP_DATA_DIR="/var/opt" \
    MY_APP_LOG_DIR="/var/log" \
    DOCKERIZE_VERSION="v0.6.1" \
    # set this to "true" to render templates on startup
    MY_TEMPLATE_ENABLE="true" \
    MY_TEMPLATE_DIR="/var/opt/templates" \
    MY_TOOL_DIR=/sbin/tools \
    # These are for KDC, overwrite this if needed
    KRB_DEFAULT_REALM="EXAMPLE.COM" \
    KRB_DEFAULT_DOMAIN_REALM="EXAMPLE.COM" \
    KRB_KDC_SERVER="localhost" \
    KRB_KDC_PORT=88 \
    KRB_ADMIN_PORT=749 \
    KRB_CONF_FILE="/etc/krb5.conf"
COPY files/share/scripts/build /my_build
RUN chmod +x /my_build/install.sh && \
    /my_build/install.sh && \
    rm -rf /my_build


COPY files/share/templates ${MY_TEMPLATE_DIR}/
COPY files/share/scripts/init ${MY_INIT_DIR}/

COPY files/share/scripts/my-tool /sbin/my-tool
COPY files/share/scripts/tools ${MY_TOOL_DIR}
RUN chmod +x /sbin/my-tool