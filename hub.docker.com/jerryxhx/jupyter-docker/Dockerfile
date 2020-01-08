# jupyter-docker
FROM debian:stable

RUN set -ex && \
    apt-get update && \ 
    apt-get install ca-certificates python3-pip -y&& \
    pip3 install --upgrade pip && \
    python3 -m pip install jupyter && \
    python3 -m pip install jupyterlab

USER = jupyter
ENV USER = jupyter
ENV HOME = /tmp
WORKDIR /tmp
EXPOSE 8888

CMD jupyter lab --no-browser
