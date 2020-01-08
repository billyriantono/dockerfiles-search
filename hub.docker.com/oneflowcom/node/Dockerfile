FROM node:8-alpine

RUN apk add --update --no-cache yarn git python3 && \
  python3 -m ensurepip && \
  rm -r /usr/lib/python*/ensurepip && \
  pip3 install --upgrade pip setuptools && \
  if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
  if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
  rm -r /root/.cache

RUN mkdir -p /opt/oneflow
WORKDIR /opt/oneflow

ADD ./requirements.txt /opt/oneflow/requirements.txt
RUN pip install -r requirements.txt
