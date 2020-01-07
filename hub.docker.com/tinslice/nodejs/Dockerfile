FROM node:12.13.1-alpine

RUN apk add --update --no-cache \
            bash git openssh \
            ca-certificates openssl \
            tar zip unzip \
            curl jq \
            ruby libressl libressl-dev build-base ruby-dev ruby-rdoc ruby-io-console ruby-irb && \
    gem install compass --no-rdoc --no-ri && \
    gem cleanup && \
    rm -rf /usr/lib/ruby/gems/*/cache/* && \
    apk del libressl-dev build-base ruby-dev && \
    rm -rf /var/cache/apk/* /tmp && mkdir -p /tmp

COPY fs/ /

RUN mkdir -p /workspace/node_modules && \
    chmod +x /prepare-env-and-run.sh

WORKDIR /workspace

ENTRYPOINT ["/prepare-env-and-run.sh"]