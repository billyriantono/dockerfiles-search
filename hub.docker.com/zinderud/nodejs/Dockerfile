ARG NODE_VERSION=10.15

FROM node:${NODE_VERSION}-alpine

LABEL author="zinderud"
LABEL description="Docker image for Node.js development"

WORKDIR /usr/src/app

USER root

RUN apk update \
  && apk upgrade \
  && apk add bash bash-completion \
  && apk add curl \
  && rm -rf /tmp/* /var/cache/apk/* \
  && sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd \
  && echo "PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '" >> ~/.bashrc

# Yarn
RUN curl --compressed -o- -L https://yarnpkg.com/install.sh | bash

# NPM setup
RUN rm -rf ~/.npm \
  && npm cache verify \
  && echo "unsafe-perm = true" >> ~/.npmrc

  # Angular
RUN yarn global add @angular/cli@$ANGULAR_VERSION

EXPOSE 4200 49153

 