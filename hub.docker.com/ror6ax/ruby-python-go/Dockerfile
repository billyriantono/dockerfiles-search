FROM codequest/ruby-golang:latest

# Pull Java JDK
RUN echo 'deb http://http.debian.net/debian jessie-backports main' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y -t jessie-backports openjdk-8-jdk maven python3-pip python3-dev
RUN update-java-alternatives --set java-1.8.0-openjdk-amd64
RUN cd /usr/local/bin \
  && ln -s /usr/bin/python3 python \
  && pip3 install --upgrade pip
