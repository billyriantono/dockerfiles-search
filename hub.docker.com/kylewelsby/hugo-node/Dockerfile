
# Use Alpine Linux as our base image so that we minimize the overall size our final container, and minimize the surface area of packages that could be out of date.
FROM circleci/node:latest

LABEL description="Docker container for building static sites with the Hugo static site generator."

MAINTAINER Kyle Welsby <kyle@mekyle.com>

ENV HUGO_VERSION=0.34

ADD https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.deb /tmp/hugo.deb
RUN sudo dpkg -i /tmp/hugo.deb \
    && sudo rm /tmp/hugo.deb

RUN sudo apt install -y rsync
