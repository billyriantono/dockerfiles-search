# Copyright 2015-2017 Ivan Krizsan
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Elastalert Docker image running on Alpine Linux.
# Build image with: docker build -t ivankrizsan/elastalert:latest .

FROM alpine

LABEL maintainer="Derek Wiedenhoeft, https://github.com/cailen"

# Set this environment variable to True to set timezone on container start.
ENV SET_CONTAINER_TIMEZONE=True \
    # Default container timezone as found under the directory /usr/share/zoneinfo/.
    CONTAINER_TIMEZONE=America/New_York \
    # URL from which to download Elastalert.
    ELASTALERT_URL=https://github.com/cailen/elastalert/archive/master.zip \
    # Directory holding configuration for Elastalert and Supervisor.
    CONFIG_DIR=/opt/config \
    # Elastalert rules directory.
    RULES_DIRECTORY=/opt/rules \
    # Elastalert configuration file path in configuration directory.
    ELASTALERT_CONFIG=${CONFIG_DIR}/elastalert_config.yaml \
    # Directory to which Elastalert and Supervisor logs are written.
    LOG_DIR=/opt/logs \
    # Elastalert home directory full path.
    ELASTALERT_HOME=/opt/elastalert \
    # Supervisor configuration file for Elastalert.
    ELASTALERT_SUPERVISOR_CONF=${CONFIG_DIR}/elastalert_supervisord.conf \
    # Alias, DNS or IP of Elasticsearch host to be queried by Elastalert. Set in default Elasticsearch configuration file.
    ELASTICSEARCH_HOST=elasticsearchhost \
    # Port on above Elasticsearch host. Set in default Elasticsearch configuration file.
    ELASTICSEARCH_PORT=9200 \
    # Use TLS to connect to Elasticsearch (True or False)
    ELASTICSEARCH_TLS=False \
    # Verify TLS
    ELASTICSEARCH_TLS_VERIFY=False \
    # ElastAlert writeback index
    ELASTALERT_INDEX=elastalert_status

WORKDIR /opt

# Install software required for Elastalert and NTP for time synchronization.
RUN apk update && \
    apk upgrade && \
    apk add ca-certificates openssl-dev openssl libffi-dev python2 python2-dev py2-pip py2-yaml gcc musl-dev tzdata openntpd wget curl && \
# Download and unpack Elastalert.
    wget -O elastalert.zip "${ELASTALERT_URL}" && \
    unzip elastalert.zip && \
    rm elastalert.zip && \
    mv e* "${ELASTALERT_HOME}"

WORKDIR "${ELASTALERT_HOME}"

# Install Elastalert.
RUN python setup.py install && \
    pip install -e . && \
# Install Supervisor.
    easy_install supervisor && \
# Create directories. The /var/empty directory is used by openntpd.
    mkdir -p "${CONFIG_DIR}" && \
    mkdir -p "${RULES_DIRECTORY}" && \
    mkdir -p "${LOG_DIR}" && \
    mkdir -p /var/empty && \
# Clean up.
    apk del python2-dev && \
    apk del musl-dev && \
    apk del gcc && \
    apk del openssl-dev && \
    apk del libffi-dev && \
    rm -rf /var/cache/apk/*

# Copy the script used to launch the Elastalert when a container is started.
COPY ./start-elastalert.sh /opt/
# Make the start-script executable.
RUN chmod +x /opt/start-elastalert.sh

# Define mount points.
VOLUME [ "${CONFIG_DIR}", "${RULES_DIRECTORY}", "${LOG_DIR}"]

# Launch Elastalert when a container is started.
CMD ["/opt/start-elastalert.sh"]
