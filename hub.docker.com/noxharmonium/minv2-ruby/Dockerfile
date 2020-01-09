FROM shippable/minv2

MAINTAINER Sean Dawson <contact@seandawson.info>

WORKDIR /home/shippable/

RUN "sudo apt-get update"
RUN "gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3"
RUN "curl -sSL https://get.rvm.io | bash -s stable --ruby"
RUN "source /home/shippable/.rvm/scripts/rvm"
RUN "rvm use ruby --default"
RUN "sudo gem install bundler"
