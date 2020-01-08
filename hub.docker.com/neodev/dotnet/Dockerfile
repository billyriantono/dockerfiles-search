FROM microsoft/dotnet
MAINTAINER neodev <dev@neoarea.com>
ENV DEBIAN_FRONTEND noninteractive
RUN mkdir -p ~/projects && cd ~/projects
RUN git clone https://github.com/neoarea/docker-dotnet.git
RUN cd docker-dotnet && dotnet restore 
RUN apt-get update
RUN apt-get install -y nano rsync