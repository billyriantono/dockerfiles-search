FROM vtrinque/base

MAINTAINER Valentin Trinqué <val.trinque@gmail.com>

# install dependencies
USER root
RUN yum clean all && yum update -y && yum install -y \
    tar

# can be overriden by setting up a new USER clause or -u option
USER app

# directory for all js-related stuff
RUN mkdir -p /home/app/env/js

# install nodejs
RUN mkdir -p /home/app/env/js/nodejs
RUN curl https://nodejs.org/dist/v4.0.0/node-v4.0.0-linux-x64.tar.gz | tar xvzf - -C /home/app/env/js/nodejs --strip-components=1
ENV PATH $PATH:/home/app/env/js/nodejs/bin

# configure npm
RUN mkdir -p /home/app/env/js/npm-global
RUN npm config set prefix '/home/app/env/js/npm-global'
ENV PATH $PATH:/home/app/env/js/npm-global/bin

