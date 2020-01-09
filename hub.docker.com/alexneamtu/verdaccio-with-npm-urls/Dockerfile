FROM verdaccio/verdaccio:latest

USER root

RUN yarn add verdaccio-npm-urls -S
 
ADD config.yaml /verdaccio/conf/config.yaml

USER $VERDACCIO_USER_UID

CMD $VERDACCIO_APPDIR/bin/verdaccio --config /verdaccio/conf/config.yaml --listen $VERDACCIO_PROTOCOL://0.0.0.0:$VERDACCIO_PORT


