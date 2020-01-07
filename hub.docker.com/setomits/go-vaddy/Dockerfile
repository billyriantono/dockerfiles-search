FROM alpine

ARG tmp_dir="/tmp/go-vaddy"
ARG vaddy_version="1.0.6"

WORKDIR ${tmp_dir}

RUN set -ex \
    && apk add --no-cache --update ca-certificates \
    && wget --quiet https://github.com/vaddy/go-vaddy/archive/v${vaddy_version}.zip \
    && unzip v${vaddy_version}.zip \
    && mv go-vaddy-${vaddy_version}/bin/vaddy-linux-64bit /usr/local/bin/vaddy

WORKDIR /

RUN set -ex && rm -rf ${tmp_dir}

CMD ["vaddy"]
