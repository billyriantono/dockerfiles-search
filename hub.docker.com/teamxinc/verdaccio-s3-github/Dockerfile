FROM verdaccio/verdaccio:3

USER root

WORKDIR /usr/local/app

ENV VERDACCIO_APPDIR=/usr/local/app \
    VERDACCIO_PROTOCOL=http \
    VERDACCIO_PORT=4873

RUN apk add --no-cache -v \
    python \
    py2-pip \
&& pip install --no-cache-dir awscli \
&& aws --version

RUN npm install --save verdaccio-github-oauth-ui
RUN npm install

COPY run-verdaccio.sh /usr/local/bin/run-verdaccio.sh
COPY s3-sync.sh /usr/local/bin/s3-sync.sh

RUN chmod +x /usr/local/bin/run-verdaccio.sh && chmod +x /usr/local/bin/s3-sync.sh

ENTRYPOINT ["/usr/local/bin/dumb-init", "--"]

CMD ["/usr/local/bin/run-verdaccio.sh"]