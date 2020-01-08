FROM jenkins
LABEL Name=npmJenkins Version=0.0.1
USER root
WORKDIR /usr/src/
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update
RUN apt-get install -y nodejs
ADD http://mirrors.jenkins.io/war-stable/latest/jenkins.war /usr/share/jenkins/
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install --no-install-recommends yarn
