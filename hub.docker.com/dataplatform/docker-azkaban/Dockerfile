FROM dataplatform/docker-hadoop-client:1.0.9-spark2
MAINTAINER MZ

EXPOSE 8443

ENV AZKABAN_VERSION="master" \
    SLF4J_BIND_VERSION="1.7.21" \
    SLF4J_BIND_NAME="slf4j-log4j12" \
    AZKABAN_DB_HOST="localhost" \
    AZKABAN_DB_PORT="3306" \
    AZKABAN_DB_USER="root" \
    AZKABAN_DB_PASS="root" \
    AZKABAN_DB_NAME="azkaban" \
    AZKABAN_DEFAULT_TZ="Etc/UTC" \
    AZKABAN_DIR="${MY_APP_DIR}/azkaban" \
    AZKABAN_REPO_URL="https://github.com/binhnv/azkaban.git"
ENV AZKABAN_SQL_DIR="${AZKABAN_DIR}/sql" \
    AZKABAN_WEB_HOME="${AZKABAN_DIR}/web" \
    AZKABAN_EXEC_HOME="${AZKABAN_DIR}/exec" \
    AZKABAN_WEB_LOG_DIR="${MY_APP_LOG_DIR}/azkaban-web" \
    AZKABAN_EXEC_LOG_DIR="${MY_APP_LOG_DIR}/azkaban-exec" \
    SLF4J_BIND_FILE="slf4j-log4j12-${SLF4J_BIND_VERSION}.jar"

WORKDIR ${AZKABAN_DIR}

COPY scripts/build /my_build
RUN /my_build/install.sh && rm -rf /my_build

COPY services ${MY_SERVICE_DIR}
COPY scripts/init ${MY_INIT_DIR}
COPY templates ${MY_TEMPLATE_DIR}
