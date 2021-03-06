# ------------------------------------------------------------------------
#
# Copyright 2019 WSO2, Inc. (http://wso2.com)
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
# limitations under the License
#
# ------------------------------------------------------------------------

# set base Docker image to AdoptOpenJDK Ubuntu Docker image
FROM adoptopenjdk/openjdk8:jdk8u192-b12
MAINTAINER Siddhi IO Docker Maintainers "siddhi-dev@googlegroups.com"

# set user configurations
# ARG USER=siddhi_user
# ARG USER_ID=802
# ARG USER_GROUP=siddhi_io
# ARG USER_GROUP_ID=802
# ARG USER_HOME=/home/${USER}
# # set dependant files directory
# ARG FILES=./files
# # set siddhi-tooling configurations
# ARG RUNTIME_SERVER=siddhi-tooling
# ARG RUNTIME_SERVER_VERSION=0.1.0
# ARG RUNTIME_SERVER_PACK=${RUNTIME_SERVER}-${RUNTIME_SERVER_VERSION}
# ARG RUNTIME_SERVER_HOME=${USER_HOME}/${RUNTIME_SERVER_PACK}
# set SIDDHI-IO EULA
ARG MOTD="\n\
Welcome to Siddhi Docker resources.\n\
------------------------------------ \n\
This Docker container comprises of a SIDDHI-IO product, running with its latest GA release \n\
which is under the Apache License, Version 2.0. \n\
Read more about Apache License, Version 2.0 here @ http://www.apache.org/licenses/LICENSE-2.0.\n"

# install required packages
RUN \
    apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        java-common \
        netcat \
        unzip \
        wget \
        dnsutils \
        telnet \
    && rm -rf /var/lib/apt/lists/* \
    && echo '[ ! -z "${TERM}" -a -r /etc/motd ] && cat /etc/motd' >> /etc/bash.bashrc; echo "${MOTD}" > /etc/motd

# create the user and group
# RUN \
#     groupadd --system -g ${USER_GROUP_ID} ${USER_GROUP} \
#     && useradd --system --create-home --home-dir ${USER_HOME} --no-log-init -g ${USER_GROUP_ID} -u ${USER_ID} ${USER}

## install the Siddhi Distribution to user's home directory

# download Siddhi Tooling Distribution

# use the Siddhi Tooling Distribution available locally
# Note: Comment the RUN command under 'Download Siddhi Distribution' heading and uncomment the below COPY command
# COPY --chown=siddhi_user:siddhi_io ${FILES}/${RUNTIME_SERVER_PACK}/ ${RUNTIME_SERVER_HOME}/

RUN mkdir /home/siddhi-runner-0.1.0
COPY ./siddhi-runner-0.1.0 /home/siddhi-runner-0.1.0
EXPOSE 8080 9443 9090
# set the user and work directory
# USER ${USER_ID}
WORKDIR /home

# set environment variables
ENV RUNTIME_SERVER_HOME=${RUNTIME_SERVER_HOME} \
    WORKING_DIRECTORY=${USER_HOME}

CMD []