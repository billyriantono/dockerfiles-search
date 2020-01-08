# Extends from the base image defined in `docker-img-angular2` repository.
FROM teatime/docker-img-angular:develop

# Install the aws command line
RUN apt-get update
RUN apt-get install python-setuptools -y
RUN apt-get install python-dev -y
RUN easy_install pip
RUN pip install awscli

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh \
    && ln -s /usr/local/bin/entrypoint.sh

WORKDIR /project

ARG BUILD_ENV="prod"

ENV BUILD_ENV=$BUILD_ENV

COPY package.json /project/package.json

COPY yarn.lock /project/yarn.lock

RUN cd /project && yarn install

ADD . /project

RUN npm run "build.$BUILD_ENV"

WORKDIR /home/app

RUN cp -a /project/. /home/app/
