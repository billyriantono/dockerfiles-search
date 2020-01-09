FROM ubuntu:14.04

MAINTAINER Zan Loy "zan.loy@stopso.com"

# Install dependencies
RUN apt-get update
RUN apt-get install -y g++ libsqlite3-dev make ruby ruby-dev
# Install mailcatcher
RUN gem install mailcatcher --no-rdoc --no-ri
# Cleanup
RUN apt-get clean

# Setup ports
EXPOSE 1025 1080

# Configure entrypoint
ENTRYPOINT /usr/local/bin/mailcatcher -f --ip 0.0.0.0
