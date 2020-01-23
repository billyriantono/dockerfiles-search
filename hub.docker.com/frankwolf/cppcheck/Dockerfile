FROM alpine:3.7
LABEL Maintainer="Frank Wolf <FrankWolf@gmx.de>" \
      Name="cppcheck" \
      Version=1.83

ARG VERSION=1.83

RUN apk add --no-cache --virtual build-dependencies \
    ca-certificates \
    g++ \
    make \
    openssl \
    pcre-dev \
    wget \
    && wget -O /tmp/cppcheck-${VERSION}.tar.gz https://github.com/danmar/cppcheck/archive/${VERSION}.tar.gz \
    && tar -zxf /tmp/cppcheck-${VERSION}.tar.gz -C /tmp \
    && cd /tmp/cppcheck-${VERSION} \
    && make install CFGDIR=/cfg HAVE_RULES=yes CXXFLAGS="-O2 -DNDEBUG -Wall -Wno-sign-compare -Wno-unused-function --static" \
    && rm /tmp/cppcheck-${VERSION}.tar.gz \
    && rm -rf /tmp/cppcheck-${VERSION} \
    && apk del build-dependencies

ARG USER=user
ARG UID=1000
ENV USER $USER

RUN mkdir /home/$USER \
  && addgroup -g $UID -S $USER \
  && adduser -u $UID -D -S -G $USER $USER \
  && chown -R $USER:$USER /home/$USER

USER $USER

VOLUME /data
WORKDIR /data

CMD ["--enable=all"]
ENTRYPOINT ["cppcheck"]
