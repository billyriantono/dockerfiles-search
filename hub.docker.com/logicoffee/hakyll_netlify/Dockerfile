FROM fpco/stack-build:lts-12.26

RUN npm cache clean                          && \
    npm install n -g                         && \
    n 10.15.0                                && \
    apt-get purge -y nodejs npm              && \
    ln -sf /usr/local/bin/node /usr/bin/node && \
    ln -sf /usr/local/bin/npm  /usr/bin/npm  && \
    npm install netlify-cli -g
