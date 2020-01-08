FROM debian:jessie-slim

# MAINTAINER Peter Wilson <pwillie@users.noreply.github.com>

# based on:
# MAINTAINER Jo Shields <jo.shields@xamarin.com>
# MAINTAINER Alexander Köplinger <alkpli@microsoft.com>

# based on dockerfile by Michael Friis <friism@gmail.com>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF

ENV MONO_VERSION 5.18.1.0

RUN echo "deb http://download.mono-project.com/repo/debian stable-jessie/snapshots/$MONO_VERSION main" > /etc/apt/sources.list.d/mono-official.list && \
   apt-get update && apt-get install -y --no-install-recommends \
   mono-runtime \
   ca-certificates-mono \
   libmono-system-core4.0-cil \
   libmono-system-management4.0-cil \
   libmono-system-runtime-caching4.0-cil \
   libmono-system-runtime-serialization4.0-cil \
   libmono-system-xml-linq4.0-cil && \
   rm -rf /var/lib/apt/lists/* /tmp/*
