# Errbot - minimum docker file

FROM python:3

MAINTAINER Mike Love mlove@michaeldlove.com

ENV ERR_HOME=/opt/errbot
ENV ERR_USER=errbot

RUN useradd -r -d $ERR_HOME $ERR_USER

RUN mkdir $ERR_HOME && \
    chown -R $ERR_USER:$ERR_USER $ERR_HOME

RUN apt-get update && \
    apt-get install -y libssl-dev libffi-dev && \
    apt-get clean

RUN pip3 install -U virtualenv setuptools

USER $ERR_USER
WORKDIR $ERR_HOME
RUN virtualenv .venv
RUN . .venv/bin/activate && \
    pip install \
    --no-cache-dir errbot sleekxmpp && \ 
    errbot --init

CMD sh -c '.  .venv/bin/activate; errbot'
