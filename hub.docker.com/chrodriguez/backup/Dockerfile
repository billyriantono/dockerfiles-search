FROM ruby:2.2.2
RUN gem install backup
RUN apt-get -y update && apt-get -y upgrade 
RUN apt-get -y install coreutils tar gzip bzip2 mysql-client rsync openssh-client
ENTRYPOINT ["backup"]
