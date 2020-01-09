FROM ruby:2.2
MAINTAINER Loïc Ambrosini <loic.ambrosini@me.com>


RUN apt-get update && apt-get install -y build-essential sqlite3 libsqlite3-dev

# install mailcatcher
RUN gem install mailcatcher -v 0.6.5 --no-ri --no-rdoc

# cleanup package manager
RUN apt-get remove --purge -y build-essential libsqlite3-dev && apt-get autoclean && apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# smtp port
EXPOSE 1025

# webserver port
EXPOSE 1080

CMD ["mailcatcher", "-f", "--ip=0.0.0.0"]