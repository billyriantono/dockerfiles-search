FROM alpine:latest

RUN apk add --no-cache \
    perl \
    perl-digest-sha1 \
    perl-io-socket-ssl \
    perl-io-socket-inet6 \
    perl-json

RUN apk add --no-cache --virtual=builddeps curl wget jq make
RUN mkdir -p /ddclient/ /var/cache/ddclient /var/run/ddclient
RUN DDCLIENT_VERSION=$(curl -ksX GET "https://api.github.com/repos/ddclient/ddclient/releases/latest" \
    | jq -r .tag_name); \
    echo "This is the $DDCLIENT_VERSION" && \
    curl -L "https://github.com/ddclient/ddclient/archive/${DDCLIENT_VERSION}.tar.gz" \
    | tar xz -C /ddclient --strip-components=1

RUN curl -L http://cpanmin.us | perl - App::cpanminus && \
    cpanm Data::Validate::IP JSON::Any && \
    apk del --purge --rdepends builddeps && \
    rm -rf /config/.cpanm /root/.cpanm /usr/local/bin/cpanm

VOLUME ["/config"]

CMD ["/ddclient/ddclient", "-foreground", "-file", "/config/ddclient.conf"]