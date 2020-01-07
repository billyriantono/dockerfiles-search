FROM buildpack-deps

ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

RUN echo "Building ..." \
    && curl -sL http://deb.nodesource.com/setup_11.x | bash - \
    && curl -sS http://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        nodejs \
        ruby \
        ruby-dev \
        yarn \
    && gem install --no-rdoc --no-ri sass -v 3.4.22 \
    && gem install --no-rdoc compass \
    && npm --global config set color false \
    && npm --global config set progress false \
    && npm install -g gulp-cli \
    && rm -rf ~/.cache/ \
    && rm -rf /var/lib/apt/lists/* \
    && true

COPY docker-entrypoint.sh /
WORKDIR /srv/src

ENTRYPOINT ["/docker-entrypoint.sh"]
