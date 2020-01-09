##################################################################
# pimatic docker file
# VERSION               0.2
##################################################################

# base image
FROM telegraf

LABEL Description="Telegraf docker image" Maintainer="trebankosta@gmail.com" Version="0.1"

####### install #######
RUN apt-get update
RUN apt-get install -y python python-dev python-requests
RUN rm -rf /var/lib/apt/lists/*
