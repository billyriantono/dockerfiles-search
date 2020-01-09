FROM node:latest
MAINTAINER R0GGER

ARG REPO="daneedk"

RUN apt-get update && apt-get install -y git && \
    git clone https://github.com/$REPO/homey.ink && \
    npm install -g serve

WORKDIR /homey.ink
EXPOSE 5000

CMD ["serve", "app"]

# BUILD CUSTOM REPOSITORY:
#
# REPO=[NAME]
# docker build --build-arg REPO=athombv -t homeydash .

# RUN (testing)
# docker run --rm --name homeydash -p 5000:5000 homeydash

# RUN (and keep it running):
# docker run -d --name homeydash --restart always -p 5000:5000 homeydash

