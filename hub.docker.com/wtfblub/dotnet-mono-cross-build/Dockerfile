FROM microsoft/dotnet:2.1.302-sdk-stretch

ENV MONO_VERSION 5.8.0.127

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb http://download.mono-project.com/repo/debian jessie/snapshots/$MONO_VERSION main" > /etc/apt/sources.list.d/mono-official.list
RUN echo "deb http://ftp.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/backports.list

RUN apt-get update \
  && apt-get install -y curl build-essential mingw-w64 cmake \
  && apt-get -t jessie-backports install -y git \
  && apt-get install -y libgtk-3-dev libwebkit2gtk-4.0-dev \
  && apt-get install -y binutils mono-devel ca-certificates-mono fsharp mono-vbnc nuget referenceassemblies-pcl \
  && rm -rf /var/lib/apt/lists/* /tmp/*
