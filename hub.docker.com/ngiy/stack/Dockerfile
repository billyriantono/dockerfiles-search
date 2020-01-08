FROM fpco/stack-build
MAINTAINER ngiy

RUN apt update
COPY . /sandbox

WORKDIR /sandbox
RUN stack setup
RUN stack install