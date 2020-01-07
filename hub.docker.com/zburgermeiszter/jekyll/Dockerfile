FROM zburgermeiszter/jekyll:base

MAINTAINER Zoltan Burgermeiszter <zoltan@burgermeiszter.com>

RUN mkdir /build

ADD build /build

WORKDIR /build

RUN jekyll build --verbose