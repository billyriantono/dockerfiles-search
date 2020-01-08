FROM ubuntu:latest
ENV TERM linux
WORKDIR /root
RUN apt update
RUN apt install -y  build-essential
RUN apt-get update
RUN apt-get install manpages-dev
RUN apt-get update
RUN apt-get install -y ruby-full
RUN apt-get update
RUN apt-get install -y ruby-dev
RUN apt update
RUN apt install -y ruby-bundler
#RUN bundle install
RUN apt-get install -y libcurl3

#RUN gem update --system
#RUN gem install rubygems-update
RUN apt install -y git
RUN git clone https://github.com/vmware/vsphere-automation-sdk-ruby

#RUN adduser rails
#RUN chsh -s /bin/bash rails
#RUN su - rails
WORKDIR /root/automation-sdk-ruby/vsphere-automation-sdk-ruby/samples/vsphere/vcenter/vm
RUN pwd
#RUN bundle install
#WORKDIR /root
#RUN gem build vsphere-automation-sdk-ruby.gemspec
RUN gem install vsphere-automation-sdk

 



