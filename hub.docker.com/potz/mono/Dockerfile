FROM debian:wheezy
MAINTAINER Potiguar Faga <potz@potz.me>

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
  && echo "deb http://download.mono-project.com/repo/debian wheezy main" > /etc/apt/sources.list.d/mono-xamarin.list \
  && apt-get update \
  && apt-get install -y mono-runtime libmono-system-core4.0-cil \
  && rm -rf /var/lib/apt/lists/* /var/tmp/*
