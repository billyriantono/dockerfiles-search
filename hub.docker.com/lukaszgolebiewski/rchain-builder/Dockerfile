FROM ubuntu:18.04

RUN apt-get update -yqq
RUN apt-get install -y apt-transport-https ca-certificates curl software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
RUN apt-get update -yqq
RUN apt install -y docker-ce sudo wget curl

RUN apt-get install cmake curl git -yqq
RUN apt-get install openjdk-8-jdk -yqq

RUN apt-get install haskell-platform -yqq
RUN apt-get install jflex -yqq

RUN curl -Ls https://git.io/sbt > /bin/sbt && chmod 0755 /bin/sbt

RUN mkdir /workdir
WORKDIR /workdir

RUN git clone https://github.com/BNFC/bnfc.git
WORKDIR bnfc/source
RUN cabal update
RUN cabal install --global
