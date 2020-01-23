# :: Header
FROM 11notes/node:stable
ENV signalCliVersion=0.6.3

# :: Run
USER root
RUN mkdir -p /signal/etc \
    mkdir -p /signal/api \
    && chmod 700 /signal/etc \
    && mkdir -p /signal/api \
    && mkdir -p /signal/ssl
RUN apk --update --no-cache add openjdk8-jre wget
RUN wget -qO - https://github.com/AsamK/signal-cli/releases/download/v${signalCliVersion}/signal-cli-${signalCliVersion}.tar.gz | tar xvzf - -C /opt \
    && mv /opt/signal-cli-${signalCliVersion} /opt/signal-cli \
    && ln -s /opt/signal-cli/bin/signal-cli /usr/local/bin/signal-cli
RUN npm install express http-auth body-parser --prefix /signal/api

ADD ./source/auth.htpasswd /signal/etc/auth.htpasswd
RUN chmod 0644 /signal/etc/auth.htpasswd
ADD ./source/main.js /signal/api/main.js

RUN apk add --no-cache --virtual .build-deps openssl \
    && openssl req -nodes -newkey rsa:4096 -keyout /signal/ssl/key.pem -out /tmp/csr.pem -subj "/C=CH/ST=ZH/L=Zurich/O=Express/OU=API/CN=NodeJS" \
    && openssl x509 -req -days 365 -in /tmp/csr.pem -signkey /signal/ssl/key.pem -out /signal/ssl/cert.pem \
    && apk del .build-deps \
    && rm /tmp/csr.pem
 
# :: Version
RUN echo "CI/CD{{$(signal-cli -v 2>&1)}}"

# :: docker -u 1000:1000 (no root initiative)
RUN chown -R node:node \
    /signal \
    /opt/signal-cli

# :: Volumes
VOLUME ["/signal/etc", "/signal/ssl"]

# :: Start
USER node
CMD ["node", "/signal/api/main.js"]