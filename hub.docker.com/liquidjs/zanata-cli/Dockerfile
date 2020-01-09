FROM node:12

RUN apt-get update \
    && apt-get -y install zeroinstall-injector openjdk-8-jre \
    && mkdir -p ~/bin \
    && yes | 0install -c add zanata-cli https://raw.githubusercontent.com/zanata/zanata.github.io/master/files/0install/zanata-cli.xml \
    && 0install -c update zanata-cli
