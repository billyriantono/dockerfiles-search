FROM node:6.10.0-alpine

RUN apk add --no-cache \
    python \
    py-pip \
    ca-certificates \
    groff \
    bash \
    git \
    openssh-client \
  && pip install --no-cache-dir --upgrade pip awscli

ENV NODE_ENV development

RUN yarn global add serverless@1.16.0

ENTRYPOINT ["/bin/bash", "-c"]