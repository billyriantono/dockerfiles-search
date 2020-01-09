FROM ethereum/client-go:v1.8.8

# install nodejs
RUN apk add --update \
    nodejs \
    && rm -rf /var/cache/apk/*

# install geth-supervisor
RUN npm --global install \
    geth-supervisor

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]
