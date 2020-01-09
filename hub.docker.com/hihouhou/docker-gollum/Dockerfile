#
# Gollum Dockerfile
#
# https://github.com/
#

# Pull base image.
FROM debian:latest

MAINTAINER hihouhou < hihouhou@hihouhou.com >

# Update & install packages for graylog
RUN apt-get update && \
    apt-get install -y make build-essential git ruby rubygems ruby-dev libicu-dev zlib1g-dev libicu-dev

#Install bundler
RUN gem install bundler gitlab-linguist

#Install gollum
RUN git clone https://github.com/gollum/gollum && \
    cd gollum && \
    bundle install && \
    rake build && \
    gem install --no-document pkg/gollum*.gem

EXPOSE 4567 

CMD ["gollum"]
