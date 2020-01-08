FROM alpine

USER root

RUN apk add --update \
  coreutils \
  bash \
  openssh \
  git \
  php7 \
  php7-openssl \
  php7-json \
  php7-phar \
  php7-mbstring \
  php7-zlib \
  wget \
  supervisor \
  ca-certificates && \
  update-ca-certificates

ADD ./scripts/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
ADD ./scripts/git_clone.sh /usr/local/bin/git_clone.sh
ADD ./scripts/install-composer.sh /usr/local/bin/install-composer.sh

ENV UID=33
ENV GID=33
RUN /usr/local/bin/install-composer.sh
RUN mkdir /var/workdir
VOLUME ["/var/workdir"]
WORKDIR /var/workdir

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD /usr/local/bin/git_clone.sh
