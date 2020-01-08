FROM alpine:3.1
MAINTAINER Vittorio_Cozzolino

# Required to execute the following commands
RUN apk update

# Install Node.js
RUN apk add nodejs

#Install Redis
RUN apk add redis

#Install git
RUN apk add git

ENTRYPOINT ["/bin/sh"]