FROM openjdk:8u151-jre-alpine
LABEL org.label-schema.schema-version = "1.0"
LABEL org.label-schema.description = "Giter8 command-line tool wrapped as a Docker image."
LABEL org.label-schema.url = "https://hub.docker.com/r/fernandoacorreia/g8/"
LABEL org.label-schema.vcs-url = "https://github.com/fernandoacorreia/giter8-docker-image"

# install pre-requisites
RUN apk --update add curl ca-certificates openssl bash

# install conscript
ENV CONSCRIPT_HOME /root/
RUN curl -s curl https://raw.githubusercontent.com/foundweekends/conscript/master/setup.sh | sh

# install giter8 using conscript
RUN ~/bin/cs n8han/giter8

# image settings
VOLUME /g8out
WORKDIR /g8out
ENTRYPOINT ["/root/bin/g8", "--force"]
