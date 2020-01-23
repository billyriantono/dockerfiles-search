#
# Copyright (c) 2009-2018. Authors: see NOTICE file.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

FROM cytomine/base:v1.1

MAINTAINER Cytomine Tean "support@cytomine.be"

ENV PATH /opt/conda/bin:$PATH

RUN apt-get update -o Acquire::CompressionTypes::Order::=gz && \
    apt-get upgrade -y && \
    apt-get -y update && \
    apt-get install -y \
        apt-transport-https \
        ca-certificates \
        curl \
        git \
        g++ \
        language-pack-en-base \
        libglib2.0-0 \
        lxc \
        iptables \
        make \
        zip

RUN cd / && wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN cd / && bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda

RUN conda install opencv shapely requests numpy --yes

RUN mkdir -p /Cytomine/

RUN cd /Cytomine/ && \
    git clone https://github.com/cytomine/Cytomine-python-client.git && \
    cd Cytomine-python-client/ && \
    git checkout refactoring

RUN cd /Cytomine/Cytomine-python-client/ && \
    python setup.py build && \
    python setup.py install

RUN cd /Cytomine/ && \
    git clone https://github.com/cytomine/Cytomine-tools.git &&\
    cd Cytomine-tools/ && \
    git checkout tags/v1.1
