From alpine:3.6

RUN apk add --update \
    nodejs \
    yarn \
    && rm -rf \
    /var/cache/* \
    /var/log/* \
    /var/tmp/* \
    && mkdir /var/cache/apk

CMD ["yarn"]
