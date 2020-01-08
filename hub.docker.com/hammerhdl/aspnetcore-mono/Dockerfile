# Stage 1
 FROM microsoft/dotnet:2.1.302-sdk-stretch AS builder
 WORKDIR /source

RUN echo "deb http://deb.debian.org/debian jessie main" |  tee /etc/apt/sources.list.d/debian-official-stable.list \
&& apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
&& apt update \
&& apt install apt-transport-https \
&& echo "deb https://download.mono-project.com/repo/debian stable-jessie main" | tee /etc/apt/sources.list.d/mono-official-stable.list \
&& apt update \
&& apt -y install mono-devel
