FROM alpine:latest
MAINTAINER Shogo Iwano <shiwano@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

RUN apk update \
  && mkdir -p /usr/share/man/man1 \
  && apk add git \
  && apk add ca-certificates \
  && apk add openssh \
  && apk add bash \
  && apk add sudo \
  && apk add shadow \
  && apk add coreutils \
  && apk add findutils \
  && apk add make \
  && apk add curl \
  && apk add tar \
  && apk add gzip \
  && apk add unzip \
  && rm -rf /var/cache/apk/* \
  && mkdir -p /var/mail \
  && groupadd --gid 3434 user \
  && useradd --uid 3434 --gid user --shell /bin/bash --create-home user \
  && echo 'user ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-user \
  && echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep

USER user
WORKDIR /home/user

ENTRYPOINT ["/bin/bash"]
