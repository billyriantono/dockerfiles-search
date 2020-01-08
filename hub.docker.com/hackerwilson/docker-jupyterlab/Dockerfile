FROM python:3.6.4-alpine3.7

ENV PYTHONUNBUFFERED 1
ENV PIP_NO_CACHE_DIR off
ENV PIP_DISABLE_PIP_VERSION_CHECK on
ENV SHELL /bin/sh

RUN set -ex \
    && echo 'https://mirrors.tuna.tsinghua.edu.cn/alpine/v3.7/main' > /etc/apk/repositories \
    && apk add --no-cache --virtual .build-deps alpine-sdk \
    && pip install pipenv -i https://pypi.tuna.tsinghua.edu.cn/simple \
    && addgroup jupyter \
    && adduser -D jupyterlab jupyter \
    && echo 'jupyterlab ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/jupyter

USER jupyterlab
WORKDIR /home/jupyterlab
COPY ./Pipfile /tmp/Pipfile
RUN set -ex \
    && cp /tmp/Pipfile /home/jupyterlab/Pipfile \
    && pipenv install --skip-lock\
    && rm -fr .cache/* \
    && mkdir -p /home/jupyterlab/data

EXPOSE 8888
CMD pipenv run jupyter lab --ip=* --port=8888 --no-browser --notebook-dir=/home/jupyterlab/data
