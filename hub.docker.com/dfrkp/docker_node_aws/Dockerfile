FROM node:alpine

## Update by pushing update to github on 17-Oct-18

RUN apk -v --update add \
  zip \
  python \
  py-pip \
  groff \
  curl \
  bash \
  gnupg \
  && pip install --upgrade awscli \
  && /bin/bash \
  && touch ~/.bashrc \
  && curl -o- -L https://yarnpkg.com/install.sh | bash \
  && apk -v --purge del py-pip curl gnupg \
  && rm /var/cache/apk/*
