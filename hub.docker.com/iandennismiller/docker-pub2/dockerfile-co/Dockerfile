FROM ubuntu:xenial
MAINTAINER iamjohnnym <j.martin0027@gmail.com>

# Install base packages
RUN apt-get update -y
RUN apt-get install -y tzdata
RUN apt-get upgrade -y
# Change TimeZone
RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime
RUN echo "Etc/UTC" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
ENV TZ=Etc/UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# Clean APK cache
RUN rm -rf /var/cache/apk/*
