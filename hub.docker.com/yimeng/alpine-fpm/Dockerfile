# Pull base image.
FROM alpine

# for china
COPY repositories /etc/apk/repositories 

COPY ./docker-entrypoint.sh /

RUN \
  apk update && \
  apk add ruby ruby-dev make gcc libc-dev && \
  gem install --no-ri --no-rdoc fpm

# Define working directory.
#VOLUME ["/data/fpm"]
#WORKDIR /data


# Define default command.
ENTRYPOINT ["/docker-entrypoint.sh"]
