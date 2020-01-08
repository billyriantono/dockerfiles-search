FROM mhart/alpine-node
RUN npm install gitbook gitbook-cli -d -g && \
    rm /usr/bin/gitbook && \
    ln -s /usr/lib/node_modules/gitbook-cli/bin/gitbook.js /usr/bin/gitbook && \
    gitbook alias /usr/lib/node_modules/gitbook