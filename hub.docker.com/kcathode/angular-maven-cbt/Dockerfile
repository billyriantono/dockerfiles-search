FROM circleci/node:10-browsers

# FROM circleci/openjdk:8-jdk-browsers

# AWD Automation lib
# FROM maven:3.5.0-jdk-8-alpine

ENV MAVEN_VERSION 3.5.4
ENV MAVEN_HOME /usr/lib/mvn
ENV PATH $MAVEN_HOME/bin:$PATH
RUN sudo curl -o apache-maven-$MAVEN_VERSION-bin.tar.gz http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz  && \
  sudo tar -zxvf apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  sudo rm apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  sudo mv apache-maven-$MAVEN_VERSION /usr/lib/mvn

RUN eval "$(ssh-agent -s)" 

RUN sudo curl -L -o cbt_tunnels.zip https://github.com/crossbrowsertesting/cbt-tunnel-nodejs/releases/download/v0.9.10/cbt_tunnels-linux-x64.zip && \
  sudo unzip cbt_tunnels.zip 

# for circleci/openjdk:8-jdk-browsers
# RUN sudo apt-get update
# RUN sudo apt-get install curl
# RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
# RUN sudo apt-get install nodejs
# RUN nodejs -v
# RUN npm -v

# # EXPOSE 80/tcp

# Confirm installs
RUN node --version
RUN npm --version
RUN mvn --version
RUN git --version


RUN echo "registry=http://artifactory.mheducation.com/artifactory/api/npm/npm-virtual" > ~/.npmrc
RUN export reset='echo -e "\e[7m TEST \e[0m"'

# RUN sudo echo "127.0.0.1       localhost.dev.learning.nonprod.mheducation.com" >> /etc/hosts

# git clone https://github.mheducation.com/MHEducation/dle-shellshocked-ui-automation-lib
# git clone https://github.mheducation.com/MHEducation/dle-ol-shell-ui


#  circleci/node:10-browsers
# # # RUN keytool -keystore /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/security/cacerts -storepass changeit -noprompt -trustcacerts -importcert -alias repo_maven_apache_org -file /kd/Desktop/repo_maven_apache_org.crt


#circleci/openjdk:8-jdk-browsers
  # keytool -keystore /docker-java-home/jre/lib/security/cacerts -storepass changeit -noprompt -trustcacerts -importcert -alias repo_maven_apache_org -file /home/kd/Desktop/repo_maven_apache_org.crt
  # sudo keytool -keystore /docker-java-home/jre/lib/security/cacerts -storepass changeit -noprompt -trustcacerts -importcert -alias learning_nonprod_mheducation_com -file /home/kd/Desktop/learning_nonprod_mheducation_com.crt


  # sudo keytool -keystore /docker-java-home/jre/lib/security/cacerts -storepass changeit -noprompt -trustcacerts -importcert -alias *_learning_nonprod_mheducation_com -file /home/kd/Desktop/*_learning_nonprod_mheducation_com.crt


  # sudo keytool -keystore /docker-java-home/jre/lib/security/cacerts -storepass changeit -noprompt -trustcacerts -importcert -alias *_mheducation_com -file /home/kd/Desktop/\*_mheducation_com.crt


#FROM circleci/node:10-browsers
#/docker-java-home
# ./shellshock.sh qastg https://my-qastg.mheducation.com/login?redirectUrl=https%3A%2F%2Fc27a6f5.ol-app-qastg.lms.nonprod.mheducation.com%2Fadmin

# 5062667b7e04