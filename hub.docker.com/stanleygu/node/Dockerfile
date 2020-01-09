FROM        ubuntu
MAINTAINER  Stanley Gu <stanleygu@gmail.com>
RUN         apt-get update -qq

# Adding PPAs
RUN         apt-get install -q -y python-software-properties
RUN         add-apt-repository -y ppa:chris-lea/node.js
RUN         add-apt-repository -y ppa:git-core/ppa
RUN         apt-get update -qq

# Installing packages
RUN         apt-get install -y -q build-essential
RUN         apt-get install -y -q git
RUN         apt-get install -y -q nodejs