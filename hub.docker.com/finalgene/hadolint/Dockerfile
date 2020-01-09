FROM alpine:3.9

LABEL maintainer="frank.giesecke@final-gene.de"

ENV HADOLINT_VERSION="v1.16.2"

# hadolint ignore=DL3018
RUN apk add --no-cache --virtual .build-deps \
        curl \
    && curl -sSLq -o /usr/local/bin/hadolint "https://github.com/hadolint/hadolint/releases/download/${HADOLINT_VERSION}/hadolint-Linux-x86_64" \
    && chmod a+x /usr/local/bin/hadolint \
    && apk del .build-deps

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD [""]
