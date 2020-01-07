FROM ubuntu:14.04
MAINTAINER Paolo Invernizzi <paolo.invernizzi@gmail.com>
# ... updated 04 april 2016

# ... first of all, update the packages ...
RUN apt-get -q update

# ... generic utilities and development tools ...
RUN apt-get -qy install \
    curl unzip xz-utils ssh \
    vim

# ... install the latest meteor ...
RUN curl -s https://install.meteor.com/ | sh

# ... fix locale for mongo: see https://github.com/meteor/meteor/issues/4019 ...
RUN locale-gen en_US.UTF-8


