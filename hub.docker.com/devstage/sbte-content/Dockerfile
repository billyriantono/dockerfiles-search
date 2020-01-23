FROM node:8-alpine

RUN apk add --update --no-cache \
    bash \
    python \
    py-pip \
    groff \
    jq \
    zip \
    curl \
    git \
    ca-certificates && \
    pip install --upgrade awscli && \
    apk -v --purge del py-pip
RUN npm install -g serverless
