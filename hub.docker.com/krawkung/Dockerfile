###########################################
# Dockerfile to build a new image
###########################################
# Base image is ubuntu
FROM ubuntu:16.04
# Auther: Mr. Arthan Thaweephonjaroen
MAINTAINER Mr. Arthan Thaweephonjaroen <arthan_t@yahoo.co.uk>
# create 'mynewdir' and 'mynewfile'
RUN mkdir mynewdir
RUN touch /mynewdir/mynewfile
# Write the message in file
RUN echo 'test only' > /mynewdir/mynewfile
