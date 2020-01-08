FROM ubuntu:12.04
MAINTAINER Yuriy Safargaliev nekto.ryadom@gmail.com
RUN apt-get update
RUN apt-get install -y wget curl gcc  make build-essential zlib1g-dev openssh-server git-core  vim python-software-properties nodejs
RUN  add-apt-repository ppa:brightbox/ruby-ng-experimental
RUN apt-get update; apt-get -y install ruby2.1 ruby2.1-dev
RUN gem install bundler
RUN git clone https://github.com/Thibaut/devdocs
RUN cd /devdocs; bundle install; thor docs:download --all
ADD run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh
EXPOSE 9292:9292
CMD ["/usr/local/bin/run.sh", "-D"]