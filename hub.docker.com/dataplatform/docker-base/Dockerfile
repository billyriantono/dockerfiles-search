FROM phusion/baseimage:0.9.18
MAINTAINER MZ

CMD ["/sbin/my_default_cmd"]
ENTRYPOINT ["/sbin/my_init", "--", "/sbin/my_startup"]

ENV TERM="xterm" \
    MY_USER="myuser" \
    MY_INIT_DIR="/etc/my_init.d" \
    MY_SERVICE_DIR="/etc/service" \
    MY_APP_DIR="/usr/local" \
    MY_APP_DATA_DIR="/var/opt" \
    MY_APP_LOG_DIR="/var/log" \
    MY_STARTUP_DIR="/etc/my_startup.d" \
    MY_TEMPLATE_DIR="/var/opt/templates" \
    MY_SERVICE_REGISTRY_DIR="/etc/my_service.d" \
    DOCKERIZE_VERSION="v0.5.0" \
    DOCKERIZE_DEFAULT_TIMEOUT="10s" \
    # These are for KDC, overwrite this if needed
    KRB_DEFAULT_REALM="EXAMPLE.COM" \
    KRB_DEFAULT_DOMAIN_REALM="EXAMPLE.COM" \
    KRB_KDC_SERVER="localhost"

ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"

VOLUME ["${MY_SERVICE_REGISTRY_DIR}"]

COPY scripts/build /my_build
RUN /my_build/install.sh && rm -rf /my_build

RUN add-apt-repository -y ppa:openjdk-r/ppa \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        openjdk-8-jdk \
        ca-certificates-java \
        unzip \
    && update-alternatives --set java ${JAVA_HOME}/jre/bin/java \
    && /var/lib/dpkg/info/ca-certificates-java.postinst configure \
    && curl -L -O -H "Cookie: oraclelicense=accept-securebackup-cookie" -k "http://download.oracle.com/otn-pub/java/jce/8/jce_policy-8.zip" \
    && unzip -oj jce_policy-8.zip -d ${JAVA_HOME}/jre/lib/security \
    && rm -f jce_policy-8.zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY scripts/init ${MY_INIT_DIR}
COPY templates ${MY_TEMPLATE_DIR}
COPY scripts/my_startup /sbin/my_startup
COPY scripts/my_service /sbin/my_service
COPY scripts/my_default_cmd /sbin/my_default_cmd
COPY scripts/my_tcp_wait /sbin/my_tcp_wait
COPY scripts/my_wait_for_file /sbin/my_wait_for_file
