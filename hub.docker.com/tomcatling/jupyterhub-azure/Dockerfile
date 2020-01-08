# An incomplete base Docker image for running JupyterHub
#
# Add your configuration to create a complete derivative Docker image.
#
# Include your configuration settings by starting with one of two options:
#
# Option 1:
#
# FROM jupyterhub/jupyterhub:latest
#
# And put your configuration file jupyterhub_config.py in /srv/jupyterhub/jupyterhub_config.py.
#
# Option 2:
#
# Or you can create your jupyterhub config and database on the host machine, and mount it with:
#
# docker run -v $PWD:/srv/jupyterhub -t jupyterhub/jupyterhub
#
# NOTE
# If you base on jupyterhub/jupyterhub-onbuild
# your jupyterhub_config.py will be added automatically
# from your docker directory.

FROM ubuntu:18.04
LABEL maintainer="Tom Catling <tomcatling@gmail.com>"
LABEL org.jupyter.service="jupyterhub"

ARG JUPYTERHUB_VERSION=0.9.4

ENV LANGUAGE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_CTYPE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update && \
    apt-get -y --no-install-recommends install python3-setuptools python3-pip nodejs npm &&\
    apt-get purge && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 install --no-cache-dir jupyterhub==${JUPYTERHUB_VERSION} azure notebook jupyterhub-simplespawner && \
    npm install -g configurable-http-proxy

COPY azure_spawner /tmp/azure_spawner
WORKDIR /tmp/azure_spawner/
RUN pip3 install --no-cache-dir .

RUN mkdir -p /srv/jupyterhub/ && \
    mkdir -p /etc/jupyterhub/
COPY jupyterhub_config.py /srv/jupyterhub/jupyterhub_config.py
COPY server_config.json /etc/jupyterhub/server_config.json

WORKDIR /srv/jupyterhub/
EXPOSE 8000
RUN useradd admin && mkdir /home/admin && useradd user && mkdir /home/user

CMD ["bash"]