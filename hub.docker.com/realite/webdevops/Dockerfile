# Base dockerfile used to customize and build realite/webdevops
# base image
FROM node:12.8.0-alpine

# install python3
RUN echo "**** install Python ****" && \
    apk add --no-cache python3 && \
    if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi && \
    \
    echo "**** install pip ****" && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache --upgrade pip setuptools wheel && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi

# install awscli
RUN pip3 install awscli

RUN apk add --no-cache curl
RUN curl -O -L https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64
RUN chmod +x jq-linux64
RUN mv jq-linux64 /usr/bin/jq

RUN yarn global add @angular/cli@8.1.3

CMD ["node"]