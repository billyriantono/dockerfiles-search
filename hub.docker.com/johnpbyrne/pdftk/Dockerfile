FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive 
RUN apt-get update && apt-get install -y pdftk imagemagick && apt-get clean
COPY assets/imagemagick/policy.xml /etc/ImageMagick-6/policy.xml
