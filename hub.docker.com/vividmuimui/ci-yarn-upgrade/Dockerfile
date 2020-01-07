FROM circleci/node:latest
MAINTAINER vivid_muimui <vivid.muimui@gmail.com>
RUN sudo sh -c 'echo "deb http://ftp.us.debian.org/debian testing main contrib non-free" >> /etc/apt/sources.list'
RUN sudo apt-get update -qq && \
    sudo apt-get install -y binutils git && \
    yarn global add https://github.com/vividmuimui/ci-yarn-upgrade
ADD build.sh /usr/local/bin/build
RUN sudo chmod +x /usr/local/bin/build
