FROM nginx:1.13-alpine

RUN apk add --no-cache dumb-init curl

COPY nginx.conf clientconfig.conf /etc/nginx/

COPY init.sh /init.sh
COPY index.html /srv/

CMD [ "dumb-init", "/init.sh" ]

HEALTHCHECK --interval=60s --timeout=5s \
    CMD curl --fail http://localhost/ && curl --fail http://localhost/php/config.php || exit 1
