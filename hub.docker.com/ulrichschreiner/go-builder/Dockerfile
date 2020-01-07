FROM golang:1.11-stretch as builder
RUN apt update \
 && apt -y install make git
WORKDIR /app

ONBUILD ARG CI_TOKEN
ONBUILD ENV CI_TOKEN=$CI_TOKEN

ADD setGitConfig.sh /setGitConfig.sh
ONBUILD RUN /setGitConfig.sh


