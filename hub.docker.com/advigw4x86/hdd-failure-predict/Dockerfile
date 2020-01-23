FROM alpine:3.2
MAINTAINER John Axel Eriksson <john.eriksson@playad.se>

RUN apk update && apk upgrade \
 && apk add --update ca-certificates wget curl build-base bash zlib-dev yaml-dev openssl-dev gdbm-dev readline-dev ncurses-dev libffi-dev \
 && curl -sSL -o ruby-install-0.5.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.5.0.tar.gz \
 && tar xzvf ruby-install-0.5.0.tar.gz \
 && cd ruby-install-0.5.0 && make install && cd .. \
 && rm -rf ruby-install-* \
 && readonly NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
 && ruby-install --cleanup -j${NPROC} --system ruby 2.1.6 -- --disable-install-rdoc \
 && gem install bundler --no-ri --no-rdoc \
 && gem install io-console --no-ri --no-rdoc \
 #&& bundle package --all \
 #&& bundle install --deployment --no-cache --retry 3 --jobs 4 --clean --local
 && apk del wget build-base linux-headers yaml-dev bash openssl-dev zlib-dev gdbm-dev readline-dev ncurses-dev libffi-dev \
 && apk add readline ncurses zlib openssl yaml libssl1.0 \
 && rm -rf /var/cache/apk/*
