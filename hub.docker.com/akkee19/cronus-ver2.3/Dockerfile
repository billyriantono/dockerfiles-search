# Version 0.1
FROM reportbee/datascience:latest
MAINTAINER Akash Srivastava <akashsrvstv@yahoo.in>
ENV DEBIAN_FRONTEND noninteractive
RUN rm -rf /var/lib/apt/lists/*

RUN apt-get clean && apt-get -y update && apt-get -y upgrade && apt-get -f install && apt-get --fix-missing install


RUN apt-get install -y  gnupg2                      \
                        libssl-dev                  \
                        apt-utils                   \
                        curl                        \
                        build-essential             \
                        software-properties-common  \
                        apt-transport-https         \
                        ca-certificates


# Mono.net
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list

# NodeJS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

RUN dpkg --configure -a                   \
    && apt-get -f install                 \
    && apt-get --fix-missing install      \
    && apt-get clean                      \
    && apt-get -y update                  \
    && apt-get -y upgrade                 \
    && apt-get -y install gcc             \
                          g++             \
                          default-jdk     \
                          default-jre     \
                          ruby            \
                          ruby-dev        \
                          perl            \
                          nodejs
RUN apt-get install -y r-base




RUN deluser nobody
RUN useradd  -M -s /bin/false nobody
RUN mkdir /temp
#RUN su - nobody
USER nobody
WORKDIR /temp
