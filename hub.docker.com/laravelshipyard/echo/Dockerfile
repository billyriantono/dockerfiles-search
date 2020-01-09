FROM node:alpine

# Add S6 to supervise our Laravel Echo process
RUN apk add --no-cache gnupg bash sqlite\
    && wget -O - "https://keybase.io/justcontainers/key.asc" | gpg --import \
    && wget -O - "https://api.github.com/repos/just-containers/s6-overlay/releases/latest" | \
           egrep "browser_download_url.+amd64.+tar.gz" | cut -d : -f 2,3 | tr -d '"' | xargs wget \
    && gpg --verify s6-overlay-amd64.tar.gz.sig s6-overlay-amd64.tar.gz \
    && tar -xzf s6-overlay-amd64.tar.gz -C / \
    && rm s6-overlay-amd64.tar.gz s6-overlay-amd64.tar.gz.sig \
    && apk del --no-cache gnupg

# Install Laravel Echo
RUN yarn global add laravel-echo-server sqlite3 bufferutil \
    && yarn cache clean --force

COPY etc /etc

WORKDIR /var/www

ENTRYPOINT [ "/init" ]