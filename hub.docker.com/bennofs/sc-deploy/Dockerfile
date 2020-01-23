FROM haskell:7.10
MAINTAINER Benno Fünfstück <benno.fuenfstueck@gmail.com>
LABEL Description="This image is used to deploy a haskell software challenge client"

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" >> /etc/apt/apt.conf
RUN apt-get install gawk curl sudo zip

RUN mkdir -p /build/sccli
WORKDIR /build
ADD https://bitbucket.org/chaosteam/sccli/get/master.tar.gz /build/sccli.tar.gz
RUN tar -xf sccli.tar.gz -C /build/sccli --strip-components=1
RUN cabal update && cabal install sccli/
