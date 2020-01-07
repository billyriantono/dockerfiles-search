FROM node:6

MAINTAINER Lars Nieuwenhuizen <l.nieuwenhuizen@developers.nl>

RUN apt-get update && apt-get install -y --no-install-recommends \
    rubygems build-essential ruby-dev ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -gq gulp bower
RUN npm install --save-dev gulp-notify
RUN gem install sass

RUN mkdir /data

WORKDIR /data

ENTRYPOINT ["/bin/bash", "-c"]