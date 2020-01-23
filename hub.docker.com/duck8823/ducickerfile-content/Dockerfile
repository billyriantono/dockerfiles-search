#
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM python:3.6-slim
SHELL ["/bin/bash", "-xc"]

ENV AIRFLOW_HOME=/usr/local/airflow
ARG AIRFLOW_VERSION=1.10.6
ARG AIRFLOW_DEPS="async_packages,aws,celery,crypto,mysql,password,redis,slack"
ARG PYTHON_DEPS=""
ARG BUILD_DEPS="freetds-dev libkrb5-dev libssl-dev libffi-dev libpq-dev git"
ARG APT_DEPS="libsasl2-dev freetds-bin build-essential default-libmysqlclient-dev apt-utils curl rsync netcat locales"

RUN set -euxo pipefail \
    && apt update \
    && if [ -n "${APT_DEPS}" ]; then apt install -y $APT_DEPS; fi \
    && apt autoremove -yqq --purge \
    && apt clean

ENV AIRFLOW_GPL_UNIDECODE yes
WORKDIR /opt/airflow
RUN set -euxo pipefail \
    && apt update \
    && if [ -n "${BUILD_DEPS}" ]; then apt install -y $BUILD_DEPS; fi \
    && if [ -n "${PYTHON_DEPS}" ]; then pip install --no-cache-dir ${PYTHON_DEPS}; fi \
    && sed -i 's/^# en_US.UTF-8 UTF-8$/en_US.UTF-8 UTF-8/g' /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 \
    && useradd -ms /bin/bash -d ${AIRFLOW_HOME} airflow \
    && pip install --no-cache-dir --upgrade pip==19.1.1 \
    && pip install --no-cache-dir apache-airflow[$AIRFLOW_DEPS]==${AIRFLOW_VERSION} \
    && apt purge --auto-remove -yqq $BUILD_DEPS \
    && apt autoremove -yqq --purge \
    && apt clean

WORKDIR $AIRFLOW_HOME
RUN mkdir -p $AIRFLOW_HOME
RUN chown -R airflow: ${AIRFLOW_HOME}

COPY scripts/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

USER airflow
ENTRYPOINT ["/entrypoint.sh"]
CMD ["--help"]