FROM hflocki/deb7

RUN apt-get update \
	&& apt-get install -y curl \
	   apt-transport-https \
	   dirmngr \
	   gnupg \ 
	&& rm -rf /var/lib/apt/lists/*

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots/4.2.1.102 main" > /etc/apt/sources.list.d/mono-xamarin.list \
	&& apt-get update \
	&& apt-get install -y mono-devel ca-certificates-mono fsharp mono-vbnc nuget screen \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /
COPY startup.sh /
RUN chmod +x startup.sh

EXPOSE 9000/tcp
EXPOSE 9000/udp

ENTRYPOINT /startup.sh ; /bin/bash
# ENTRYPOINT ["/bin/bash"]
