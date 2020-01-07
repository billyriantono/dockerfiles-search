FROM debian:unstable
ENV DEBIAN_FRONTEND="noninteractive"
RUN apt-get update -yqq && apt-get install -yqq curl unzip findutils make git
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
