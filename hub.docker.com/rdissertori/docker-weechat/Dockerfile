FROM alpine:3.10.2
EXPOSE 8001 9000 9001
ENV VERSION=2.6 UID=1000
VOLUME ["/home/roman/Xdcc","/home/roman/.weechat"]
RUN apk update \
&& apk upgrade \
&& apk add curl g++ make cmake pkgconfig \
tcl-dev nodejs lua-dev perl-dev ruby-dev ncurses-dev curl-dev zlib-dev libgcrypt-dev libsodium-dev gnutls-dev \
gettext ca-certificates aspell python gnutls libgcrypt perl tcl ruby lua \
&& adduser -u ${UID} -h /home/roman -D roman roman \
&& curl https://weechat.org/files/src/weechat-${VERSION}.tar.gz | tar xz \
&& cd weechat-${VERSION} \
&& mkdir build \
&& cd build \
&& cmake .. \
&& make \
&& make install \
&& apk del g++ make cmake pkgconfig \
tcl-dev lua-dev perl-dev ruby-dev ncurses-dev curl-dev zlib-dev libgcrypt-dev libsodium-dev gnutls-dev \
&& rm -rf /var/cache/apk/* \
&& rm -rf /tmp/*
USER roman
WORKDIR /home/roman
ENTRYPOINT ["weechat"]
