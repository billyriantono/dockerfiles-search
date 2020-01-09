  
##################################################################
# deconz docker file
# VERSION               0.1
##################################################################

# base image
FROM marthoc/deconz

LABEL Description="deconz docker image" Maintainer="trebankosta@gmail.com" Version="0.1"

####### install #######
RUN apt-get update
RUN apt-get install -y python python-dev python-requests vim
RUN rm -rf /var/lib/apt/lists/*
