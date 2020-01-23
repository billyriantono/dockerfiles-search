FROM composer as compose

RUN git clone --depth 1 https://github.com/wikimedia/mediawiki-extensions-LinkedWiki /LinkedWiki &&\
    cd /LinkedWiki && \
    composer install --no-dev &&\
    apk add  --no-cache yarn &&\
    yarn install --production=true

FROM wikibase/wikibase:1.33
COPY --from=compose /LinkedWiki /var/www/html/extensions/LinkedWiki
COPY extra-entrypoint-run-first.sh /extra-entrypoint-run-first.sh

