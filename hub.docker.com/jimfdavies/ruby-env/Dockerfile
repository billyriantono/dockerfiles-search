FROM ruby:latest

MAINTAINER jimfdavies@gmail.com

RUN apt-get update && apt-get install vim -y
RUN gem update && gem install rspec cucumber rubocop

COPY .bashrc .gitconfig /root/
WORKDIR /code

CMD ["/bin/bash"]
