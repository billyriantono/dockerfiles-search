FROM ubuntu:xenial

MAINTAINER Antonio "acdc" Jr. <acdcjunior@gmail.com>

# Travis Gem
RUN apt-get update && \
	apt-get -y install git build-essential ruby ruby-dev && \
	gem install travis

# Heroku
# software-properties-common is required so apt-add-repository is available [https://stackoverflow.com/a/32487026/1850609]
# curl to download release.key below
# apt-transport-https due to error E: The method driver /usr/lib/apt/methods/https could not be found. [https://askubuntu.com/a/211531]

RUN apt-get -y install software-properties-common curl apt-transport-https && \
    add-apt-repository "deb https://cli-assets.heroku.com/branches/stable/apt ./" && \
    curl -L https://cli-assets.heroku.com/apt/release.key | apt-key add - && \
    apt-get update && \
    apt-get -y install heroku
