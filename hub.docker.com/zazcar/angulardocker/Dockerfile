FROM node:8.9.4

ENV ANGULAR_CLI_VERSION=1.5.4 \
    YARN_VERSION=1.5.1

RUN apt-get -qq update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -qq sudo python-dev python-pip && \
  pip install -q awscli && \
  apt-get clean && \
  DEBIAN_FRONTEND=noninteractive apt-get purge -y --auto-remove && \
  rm -rf /var/lib/apt/lists/*


# adds the group
RUN echo "node ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers


# default user to run commands on the container, also all RUN commands from this point are executed
# with this user
USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

## More setup
RUN npm install -g @angular/cli@$ANGULAR_CLI_VERSION -q --no-progress --loglevel warn


## yarn setup

RUN curl -o - -L https://yarnpkg.com/install.sh | bash -s -- --version $YARN_VERSION


RUN mkdir /home/node/app


WORKDIR /home/node/app
