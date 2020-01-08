FROM debian
MAINTAINER Paolo Bosetti
LABEL name=debian-build
VOLUME /root/build
WORKDIR /root/build
COPY bash_profile /root/.bash_profile
RUN apt-get update && apt-get install -y \
  bsdmainutils \
  build-essential clang bison cmake \
  ruby ruby-dev \
  git \
  vim \
  libyaml-0-2 libyaml-dev \
  libpcre3 libpcre3-dev \
  libatlas-base-dev libatlas-dev \
  libblas3 libblas-common libblas-dev \
  && rm -rf /var/lib/apt/lists/*
RUN gem install erubis pry colorize rake --no-rdoc --no-ri
CMD ["/bin/bash", "-li"]
