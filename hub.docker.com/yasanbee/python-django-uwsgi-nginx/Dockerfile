# Copyright 2019 YaSanBee
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# [ GitHub ] - YaSanBee/Dockerfiles/Python/3.6.8/Django-uWSGI-Nginx
#
# [ DockerHub ] - yasanbee/python-django-uwsgi-nginx
#
# VERSION [ 1.1.0 ]

FROM    python:3.6.8

MAINTAINER    YaSanBee    <YaSanBee.ZERG@gmail.com>

ENV    DOCKER_HOME /home/docker

ADD    ./Config/* ${DOCKER_HOME}/Config/

# Install Nginx & Supervisor
RUN    apt-key add ${DOCKER_HOME}/Config/nginx_signing.key \
                    && echo "deb http://nginx.org/packages/debian/ stretch nginx" >> /etc/apt/sources.list \
                    && echo "deb-src http://nginx.org/packages/debian/ stretch nginx" >> /etc/apt/sources.list \
                    && apt-get update \
                    && apt-get install -y nginx supervisor \
                    && rm -rf /var/lib/apt/lists/*

# Setup Nginx & Supervisor
RUN    rm -rf /etc/nginx/conf.d/* \
                    && cp ${DOCKER_HOME}/Config/Nginx-uWSGI-Django.conf /etc/nginx/conf.d/ \
                    && cp ${DOCKER_HOME}/Config/Supervisor.conf /etc/supervisor/conf.d/ \
                    && echo "daemon off;" >> /etc/nginx/nginx.conf

# Install uWSGI
RUN    pip install uwsgi

# Setup uWSGI
RUN    useradd uwsgi -s /bin/false \
                    && mkdir /var/log/uwsgi \
                    && chown -R uwsgi:uwsgi /var/log/uwsgi \
                    && mkdir /var/run/ZergPools \
                    && chown -R uwsgi:uwsgi /var/run/ZergPools \
                    && mkdir /var/run/uwsgi \
                    && chown -R uwsgi:uwsgi /var/run/uwsgi

# Install Project & Django
ONBUILD    ADD    . ${DOCKER_HOME}/Project/
ONBUILD    RUN    if [ -f ${DOCKER_HOME}/Project/requirements.txt ]; \
                                            then pip install -r ${DOCKER_HOME}/Project/requirements.txt; fi

EXPOSE    8080

CMD    ["/bin/bash"]
