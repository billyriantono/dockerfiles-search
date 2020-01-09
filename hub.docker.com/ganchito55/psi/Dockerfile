FROM node:11-alpine

RUN set -x \
    && apk update \
    && apk upgrade \
    && apk add --no-cache \
    dumb-init \    
    && npm install --global psi \
      \
      # Cleanup
      #&& apk del --no-cache make gcc g++ python binutils-gold gnupg libstdc++ \
      && rm -rf /usr/include \
      && rm -rf /var/cache/apk/* /root/.node-gyp /usr/share/man /tmp/* \
&& echo 

ENTRYPOINT ["psi"]