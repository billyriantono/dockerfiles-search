FROM debian

RUN set -x \
  && apt update \
  && apt install -yqq \
    yarn

COPY ./public/ /code/public/
COPY ./src/ /code/src/
COPY ./package.json /code/package.json