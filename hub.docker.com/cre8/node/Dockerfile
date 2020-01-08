FROM node:7

RUN set -x \
        && apt-key adv --fetch-keys http://dl.yarnpkg.com/debian/pubkey.gpg \
        && echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
        && apt-get update && apt-get install -y --no-install-recommends \
            yarn

ENV PATH $PATH:$HOME/.yarn/bin
