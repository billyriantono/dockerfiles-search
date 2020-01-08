FROM ruby:2.3.1

RUN mkdir /code
WORKDIR /code

RUN apt-get update -y
RUN apt-get install xvfb iceweasel openjdk-7-jre -y

RUN wget http://selenium-release.storage.googleapis.com/2.53/selenium-server-standalone-2.53.0.jar

RUN gem install bundler --no-ri --no-rdoc
RUN gem install therubyracer --no-ri --no-rdoc