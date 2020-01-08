FROM itfarm/baseimage:develop

ENV ENABLE_REGISTRY_MIRROR="false" REGISTRY_MIRROR=""

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
	nodejs \
        yarn \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/

RUN npm install -g vue-cli eslint

COPY init.sh /etc/my_init.d/init.sh

EXPOSE 8080 3000
