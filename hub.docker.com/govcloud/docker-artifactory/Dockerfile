
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements. See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership. The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License. You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied. See the License for the
# specific language governing permissions and limitations
# under the License.
#

FROM docker.bintray.io/jfrog/artifactory-pro:6.5.13
LABEL maintainer="William Hearn <william.hearn@canada.ca>"
LABEL site="https://jfrog.com/artifactory"

# Set vars
ENV ARTIFACTORY_USER_NAME=artifactory \
    ARTIFACTORY_USER_ID=1030 \
    ARTIFACTORY_HOME=/opt/jfrog/artifactory \
    ARTIFACTORY_DATA=/var/opt/jfrog/artifactory \
    ARTIFACTORY_EXTRA_CONF=/artifactory_extra_conf \
    RECOMMENDED_MAX_OPEN_FILES=32000 \
    MIN_MAX_OPEN_FILES=10000 \
    RECOMMENDED_MAX_OPEN_PROCESSES=1024 \
    POSTGRESQL_VERSION=9.4.1212

# Override entrypoint and fix cp to support symbolic links
# COPY scripts/entrypoint-artifactory.sh /

# Add extra plugins
COPY plugins/* /tmp/plugins/

# Expose Tomcat's port
EXPOSE 8081

# Start the simple standalone mode of Artifactory
# ENTRYPOINT ["/entrypoint-artifactory.sh"]
