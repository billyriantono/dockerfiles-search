#
# This is our base image build file
#
# Usage:  docker build -t chromeriver/base:dev base
#

FROM buildpack-deps:sid-curl

# Because this is a BASE image, run the apt-get update and upgrade
RUN apt-get update && apt-get install -y unzip && apt-get -y upgrade && apt-get clean && rm -rf /var/lib/apt/lists/*
