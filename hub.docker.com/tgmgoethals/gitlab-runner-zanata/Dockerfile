FROM node:10.16.0-stretch-slim

# update sources list
RUN apt-get clean
RUN apt-get -qq -y update
# Install openjdk8
RUN mkdir -p /usr/share/man/man1
RUN apt-get -qq -y install openjdk-8-jdk-headless

# Install i18next for format conversions
RUN npm install i18next-conv -g

# Install zanata-cli
RUN apt-get -qq -y install 0install-core --no-install-recommends
RUN apt-get -qq -y install unzip
RUN yes | 0install -c add zanata-cli https://raw.githubusercontent.com/zanata/zanata.github.io/master/files/0install/zanata-cli.xml
RUN 0install -c update zanata-cli