#Download base image ubuntu 14.04
FROM ubuntu:14.04

LABEL maintainer="Johnathan Wong <johnathanwong4@gmail.com>" \
name=jowong4/abyss-docker \
org.label-schema.description="AbySS Build Environment"

RUN apt-get update -qq \
&& apt-get install -qq software-properties-common \
&& add-apt-repository -y ppa:ubuntu-toolchain-r/test \
&& apt-get install -qq autoconf automake libboost-dev libgtest-dev libopenmpi-dev libsparsehash-dev make pandoc
