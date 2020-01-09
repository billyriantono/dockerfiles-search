FROM ubuntu:disco

USER root


RUN apt-get update
RUN apt-get install -y bash
RUN apt-get install -y git-lfs
RUN apt-get install -y g++
RUN apt-get install -y make
RUN apt-get install -y libgmp-dev
RUN apt-get install -y ruby-full && gem install fastlane -NV
RUN apt-get install -y jq
RUN apt-get install -y curl
RUN apt-get install -y openjdk-8-jdk
RUN apt-get install -y yarn

RUN useradd -ms /bin/bash circleci
USER circleci

