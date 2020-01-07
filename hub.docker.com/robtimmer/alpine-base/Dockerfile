# Build from alpine image, tag latest
FROM alpine

# Set maintainer info
MAINTAINER Rob Timmer <rob@robtimmer.com>

# Install basic packages
# Install basic packages
RUN apk add --update bash \
                     libressl \
                     curl \
                     fping \
                     libcap

# Clear cache
RUN rm -rf /var/cache/apk/* && mkdir /opt 
