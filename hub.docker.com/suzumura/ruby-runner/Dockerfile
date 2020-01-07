FROM ruby:latest

WORKDIR /root
RUN apt-get update -y && apt-get install -y libav-tools libimage-exiftool-perl imagemagick ghostscript
ENV BUNDLE_PATH=/root/.bundle.docker
ENV BUNDLE_APP_CONFIG=/root/.bundle.docker
VOLUME ["/root"]
