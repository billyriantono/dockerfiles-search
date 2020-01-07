# dev-integration image to build Java & JS kurento projects
#
# VERSION	6.0.0

FROM	maven:3.3-jdk-7
MAINTAINER Patxi Gortázar <patxi.gortazar@gmail.com>

RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates
RUN mkdir /nodejs && curl https://nodejs.org/dist/v0.10.40/node-v0.10.40-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
ENV PATH $PATH:/nodejs/bin

RUN npm -g install bower

RUN useradd -ms /bin/bash build
RUN cd && cp -R .bashrc .profile /home/build
RUN chown -R build:build /home/build
USER build
ENV HOME /home/build
