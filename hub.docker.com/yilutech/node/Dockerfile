FROM alpine:3.7

ENV NVM_VERSION=v0.33.6 NODE_VERSION=v6.14.3 ENV=/root/.ashrc

RUN apk add --update --no-cache curl bash \
    ca-certificates openssl coreutils \
 && apk add --update --no-cache --virtual build-dependencies ncurses python2 \
    make gcc g++ libgcc linux-headers \
 && cd /root \
 && curl -o- https://raw.githubusercontent.com/creationix/nvm/$NVM_VERSION/install.sh | bash \
 && echo "#NVM Setup" >> $ENV \
 && echo 'export NVM_DIR="$HOME/.nvm"' >> $ENV \
 && echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm' >> $ENV \
 && source $ENV \
 && nvm install -s $NODE_VERSION --fully-static \
 && rm -rf /root/.nvm/.cache/src/node-$NODE_VERSION \
 && apk del build-dependencies \
 && rm -rf /tmp/* /var/cache/apk/*