ARG NODE_VERSION=12.7.0
FROM node:${NODE_VERSION}-alpine

WORKDIR /root

ENV PATH=$PATH:/root/.local/bin

RUN npm config set unsafe-perm true && \
    npm i -g yarn

RUN apk update && apk add --no-cache \
    bash \
    curl \
    docker \
    git \
    zip

RUN apk add --no-cache python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

ARG AWSCLI_VERSION=1.16.207
RUN pip install --upgrade pip && pip install --user awscli==${AWSCLI_VERSION}

WORKDIR /root
VOLUME /root/.aws

CMD ["/bin/sh"]
