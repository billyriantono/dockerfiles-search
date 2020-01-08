FROM debian:stable-slim

MAINTAINER IPP

RUN apt --yes update
RUN apt --yes upgrade
RUN apt --yes install texlive-full latexmk

# From https://github.com/docker-library/python/blob/master/Dockerfile-debian.template
ENV LANG C.UTF-8
