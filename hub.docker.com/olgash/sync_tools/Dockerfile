FROM ubuntu:18.04

MAINTAINER Olga Shalganova, olga.shalganova@jetbrains.com

RUN apt-get update -y && apt-get install -y ssh rsync jq python3-pip curl

RUN pip3 install awscli --upgrade --user
