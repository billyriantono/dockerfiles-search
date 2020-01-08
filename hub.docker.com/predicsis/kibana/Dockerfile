#
# Kibana Dockerfile
#
# https://github.com/predicsis/kibana
#

# Pull base image.
FROM debian:wheezy
MAINTAINER wnkz

ENV KB_PKG_NAME kibana-4.1.1-linux-x64

RUN apt-get update && apt-get install -qy wget

# Install Kibana.
RUN \
  cd / && \
  wget --no-check-certificate https://download.elastic.co/kibana/kibana/$KB_PKG_NAME.tar.gz && \
  tar xvzf $KB_PKG_NAME.tar.gz && \
  rm -f $KB_PKG_NAME.tar.gz && \
  mv /$KB_PKG_NAME /kibana

# Mount kibana.yml config.
ADD config/kibana.yml /kibana/config/kibana.yml

# Define working directory.
WORKDIR /kibana

# Define default command.
CMD ["/kibana/bin/kibana"]

# Expose ports.
#   - 5601: Kibana
EXPOSE 5601
