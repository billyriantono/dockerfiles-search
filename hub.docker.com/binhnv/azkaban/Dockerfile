FROM binhnv/hadoop-eco:1.0
LABEL maintainer="Binh Van Nguyen<binhnv80@gmail.com>"

ENV AZKABAN_VERSION="3.11.0" \
    SLF4J_BIND_VERSION="1.6.6" \
    SLF4J_BIND_NAME="slf4j-log4j12" \
    AZKABAN_DB_HOST="mysql" \
    AZKABAN_DB_PORT="3306" \
    AZKABAN_DB_USER="root" \
    AZKABAN_DB_PASS="root" \
    AZKABAN_DB_NAME="azkaban" \
    AZKABAN_DEFAULT_TZ="Etc/UTC" \
    AZKABAN_DIR="${MY_APP_DIR}/azkaban" \
    AZKABAN_REPO_URL="https://github.com/azkaban/azkaban.git"

ENV AZKABAN_OPTS="-Xmx256m" \
    AZKABAN_ENABLE_SSL="false" \
    AZKABAN_INIT_SCHEMA="false" \
    AZKABAN_SQL_DIR="${AZKABAN_DIR}/azkaban-sql" \
    AZKABAN_WEB_HOME="${AZKABAN_DIR}/azkaban-web-server" \
    AZKABAN_EXEC_HOME="${AZKABAN_DIR}/azkaban-exec-server" \
    AZKABAN_LOG_DIR="${MY_APP_LOG_DIR}/azkaban" \
    SLF4J_BIND_FILE="${SLF4J_BIND_NAME}-${SLF4J_BIND_VERSION}.jar"

WORKDIR ${AZKABAN_DIR}
COPY files/share/scripts/build /my_build
RUN chmod +x /my_build/install.sh && \
    /my_build/install.sh && \
    rm -rf /my_build


COPY files/share/services ${MY_SERVICE_DIR}/
COPY files/share/templates ${MY_TEMPLATE_DIR}/
COPY files/share/scripts/init ${MY_INIT_DIR}/

