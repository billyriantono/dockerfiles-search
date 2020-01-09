FROM buildpack-deps:jessie-curl

ENV OAUTH2_PROXY 2.0.1
ENV GOLANG 1.4.2

ENV BITLY /opt/bitly
RUN mkdir -p $BITLY/archive $BITLY/oauth2_proxy

ENV PACKAGE oauth2_proxy-$OAUTH2_PROXY.linux-amd64.go$GOLANG.tar.gz

RUN wget https://github.com/bitly/oauth2_proxy/releases/download/v$OAUTH2_PROXY/$PACKAGE --output-document=$BITLY/archive/oauth2_proxy.tar.gz

RUN tar -xzvf $BITLY/archive/oauth2_proxy.tar.gz --directory $BITLY/oauth2_proxy --strip-components=1

WORKDIR $BITLY

ENTRYPOINT [ "oauth2_proxy/oauth2_proxy" ]
