FROM circleci/ruby:2.4-node

########################################
ENV APP_HOME /myapp
ENV BUNDLE_PATH /cache
########################################
RUN sudo su -c "printf \"deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main\" > /etc/apt/sources.list"
RUN sudo apt-get update -qq && sudo apt-get install -y build-essential

# for postgres
RUN sudo apt-get install -y libpq-dev

# for nokogiri
RUN sudo apt-get install -y libxml2-dev libxslt1-dev

# for pdftk
RUN sudo apt-get install -y pdftk
USER root

RUN sudo mkdir $APP_HOME

WORKDIR $APP_HOME

ADD . $APP_HOME
