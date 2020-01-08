FROM node:4
RUN git clone https://github.com/jcoglan/vault.git /usr/local/src/vault \
 && cd /usr/local/src/vault \
 && git submodule init && git submodule update \
 && npm link
ENTRYPOINT ["/usr/local/bin/vault"]
VOLUME /root/.vault
