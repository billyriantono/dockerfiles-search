FROM ubuntu:17.10

RUN apt-get update -qq
RUN apt-get install -qq software-properties-common python-software-properties

RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update -qq

RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
# RUN debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
RUN apt-get install -y maven oracle-java8-installer

COPY . /src/warmup
WORKDIR /src/warmup
RUN mvn dependency:go-offline -Dmaven.test.skip=true
RUN mvn dependency:resolve-plugins -Dmaven.test.skip=true
RUN rm -rf ./src/

# If you're reading this and have any feedback on how this image could be
#   improved, please open an issue or a pull request so we can discuss it!