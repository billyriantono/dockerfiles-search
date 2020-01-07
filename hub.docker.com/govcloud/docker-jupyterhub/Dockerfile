
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

FROM jupyterhub/k8s-hub:f8dec3f
LABEL maintainer="William Hearn <william.hearn@canada.ca>"
LABEL site="https://z2jh.jupyter.org"

ARG NB_USER=jovyan
ARG NB_UID=1000
ARG HOME=/home/jovyan

USER root

COPY conf/jupyterhub/ /usr/local/share/jupyterhub/

ARG JUPYTERHUB_VERSION=0.9.*

COPY requirements.txt /tmp/requirements.txt

RUN pip3 install --no-cache-dir \
         jupyterhub==${JUPYTERHUB_VERSION} \
         -r /tmp/requirements.txt

COPY jupyterhub_config.py /srv/jupyterhub_config.py

USER ${NB_USER}

# JupyterHub API port
EXPOSE 8081

# USER ${NB_USER}
CMD ["jupyterhub", "--config", "/srv/jupyterhub_config.py"]
