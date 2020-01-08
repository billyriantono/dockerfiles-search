FROM jenkinsci/ssh-slave
LABEL MAINTAINER="Victor Soria <vjsoria@gmail.com>"
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y build-essential
