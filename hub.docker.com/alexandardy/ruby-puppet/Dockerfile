# for puppet unit testing
FROM ubuntu:latest
MAINTAINER Alex Y

RUN apt-get update
RUN apt-get install -y curl vim git
RUN curl -sSL https://get.rvm.io | bash -s stable --ruby
ENV PATH /usr/local/rvm/scripts:/usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
RUN /bin/bash -c "source /usr/local/rvm/scripts/rvm; gem install puppet puppet-lint puppet-syntax rake rspec-core rspec-puppet r10k"
CMD echo "Please run 'source /usr/local/rvm/scripts/rvm'"
