# FROM davisvansant/alpine-base

# RUN apk update && apk upgrade
# RUN apk add --no-cache --virtual .build-deps \
#   coreutils \
#   make \
#   zlib-dev \
#   openssl-dev \
#   openssl \
#   gcc \
#   linux-headers \
#   build-base \
#   && wget -O ruby-2.4.0.tar.gz https://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.0.tar.gz \
#   && tar -zxvf ruby-2.4.0.tar.gz \
#   && cd ruby-2.4.0 \
#   && ./configure --disable-install-doc --disable-install-rdoc --disable-install-capi  \
#   && make \
#   && make install \
#   && apk del .build-deps \
#   && rm -rf ruby-2.4.0*

FROM davisvansant/alpine-base:onbuild

RUN wget -O ruby-2.4.0.tar.gz https://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.0.tar.gz \
  && tar -zxvf ruby-2.4.0.tar.gz \
  && cd ruby-2.4.0 \
  && ./configure --disable-install-doc --disable-install-rdoc --disable-install-capi  \
  && make \
  && make install \
  && cd / \
  #&& apk del .build-deps \
  && rm -rf ruby-2.4.0*

CMD ["irb"]
