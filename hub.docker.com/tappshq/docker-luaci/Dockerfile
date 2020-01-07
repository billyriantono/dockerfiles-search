FROM debian

RUN apt-get update \
    && apt-get install -y \
        curl \
        gnupg2 \
    && curl -sL https://deb.nodesource.com/setup_9.x | bash - \
    && apt-get install -y \
        git \
        liblua5.1-dev \
        luarocks \
        nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN luarocks install ldoc
RUN luarocks install luacheck
RUN luarocks install busted
RUN luarocks install lua-cjson
RUN npm install -g lua-fmt

ADD compare-luafmt.sh /usr/local/bin/compare-luafmt.sh
RUN chmod 755 /usr/local/bin/compare-luafmt.sh
