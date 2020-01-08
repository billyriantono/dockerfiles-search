FROM ubuntu

MAINTAINER stalker69sok@gmail.com

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
	echo "deb http://download.mono-project.com/repo/ubuntu stable-xenial main" | tee /etc/apt/sources.list.d/mono-official-stable.list 

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y \
	ca-certificates \
	mono-complete \
	wget \
	mono-devel \
	nunit \
	nunit-console
	
RUN wget https://dist.nuget.org/win-x86-commandline/latest/nuget.exe -P /usr/bin

RUN echo '#!/bin/sh' > /usr/bin/nuget && \
	echo 'exec /usr/bin/mono /usr/bin/nuget.exe "$@"' >> /usr/bin/nuget && \
	chmod +x /usr/bin/nuget

RUN ln -s /usr/bin/xbuild /usr/bin/msbuild.exe
