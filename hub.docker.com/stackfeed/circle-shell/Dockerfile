FROM docker:stable

ENV TERM=xterm-256color
RUN \
  apk add --no-cache --update curl bash gnupg tar jq git openssh-client sudo make && \
  adduser -u 3434 -s /bin/bash -D circleci \
    && echo 'circleci ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-circleci \
    && echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep \
    && chmod 440 /etc/sudoers.d/50-circleci

USER circleci
