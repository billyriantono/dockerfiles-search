FROM jenkins/jenkins:lts

USER root

# Update
RUN apt-get update
RUN apt-get -y upgrade

# Install Node.JS LTS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get -y install nodejs

# Install Yarn Stable
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get -y install yarn

# Install OpenJDK 8 LTS
RUN apt-get -y install openjdk-8-jdk

# Install Maven
RUN apt-get -y install maven

USER jenkins