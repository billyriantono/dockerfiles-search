from ubuntu

ENV PATH=$PATH:/opt/ruby/bin/
RUN apt-get update
RUN apt-get install wget curl tar bzip2 gcc make libsqlite3-dev graphviz -y
RUN wget -O ruby-install-0.6.1.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.1.tar.gz
RUN tar -xzvf ruby-install-0.6.1.tar.gz
RUN cd ruby-install-0.6.1/ && make install

RUN ruby-install --install-dir /opt/ruby ruby 

RUN wget -O rubygems.tgz https://rubygems.org/rubygems/rubygems-2.7.6.tgz
RUN tar -zxvf rubygems.tgz
RUN cd rubygems-2.7.6 && ruby setup.rb

RUN gem update --system
RUN gem install rails
RUN gem install sqlite3

RUN apt-get install -y python3 python3-pip python3-dev
RUN pip3 install faker
RUN pip3 install requests

