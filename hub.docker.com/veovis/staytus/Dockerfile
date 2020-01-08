FROM ruby:2.5-alpine
LABEL Author Tim Perry <pimterry@gmail.com>

COPY . /opt/staytus

RUN set -xe; \
    cd /opt/staytus; \
    apk add --no-cache mariadb-connector-c nodejs tzdata; \
    apk add --no-cache --virtual=_build alpine-sdk mariadb-dev; \
    #rm Gemfile.lock; \
    bundle install --without development:test; \
    apk del _build

ENTRYPOINT /opt/staytus/docker-start.sh

# Persists copies of other relevant files (DB config, custom themes). Contents of this are copied 
# to the relevant places each time the container is started
VOLUME /opt/staytus/persisted

EXPOSE 5000