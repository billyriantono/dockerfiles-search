FROM google/cloud-sdk

# Install nodejs10
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y  \
        nodejs \
        yarn \
        wget \
        jq && \
    apt-get -qyy autoremove && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get -qyy clean
