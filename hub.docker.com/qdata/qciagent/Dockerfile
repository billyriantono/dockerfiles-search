FROM ubuntu:16.04

ENV CONSUL_TEMPLATE_VERSION=0.19.3 

#Setup
RUN apt-get update
RUN apt-get install -y curl unzip gpgv2 tar wget
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
  echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.0.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential software-properties-common locales libbz2-dev zlib1g-dev

RUN \
  apt-get install -y language-pack-en-base && \
  locale-gen en_US.UTF-8 && \
  export LANG=en_US.UTF-8 && \
  LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get update

RUN \
  apt-get install -y curl unzip jq php7.1 php7.1-cli php7.1-mysql php7.1-mcrypt php7.1-bcmath php7.1-curl php7.1-xml php7.1-mbstring php7.1-gd php7.1-bz2 php7.1-zip git git-core git-extras lftp mongodb-org=3.0.12 mongodb-org-server=3.0.12 mongodb-org-shell=3.0.12 mongodb-org-mongos=3.0.12 mongodb-org-tools=3.0.12 && \ 
  echo "extension=mcrypt.so" >> /etc/php/7.1/cli/php.ini && \
  # Node version set 4.X to support Quantum Deployment
  curl -sL https://deb.nodesource.com/setup_9.x | bash - && \
  apt-get install -y nodejs && \
  rm -rf /var/lib/apt/lists/* 
  
#Install Consul Template
RUN ( curl https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip -o /tmp/consul_template.zip && unzip /tmp/consul_template.zip && mv consul-template /usr/bin && rm -rf /tmp/* )

#Install Python
RUN apt-get update
RUN apt-get install -y python-pip python-dev build-essential
RUN apt-get install -y docker.io

#Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#Install front-end dependencies
RUN npm install -g grunt-cli
RUN npm install -g bower
RUN npm install -g gulp
RUN npm install -g gulp-cli
RUN npm install -g @angular/cli
RUN pip install aws-sam-cli

#Configure deploy by python
RUN mkdir cmdtools
COPY cmdtools/ cmdtools/
RUN cd cmdtools/deploytools && pip install -r requirements.txt

#Configure deploy script
ADD deploy.bash deploy.bash
RUN chmod +x deploy.bash

#Configure sass
RUN wget -O sass.tar.gz https://github.com/sass/dart-sass/releases/download/1.1.1/dart-sass-1.1.1-linux-x64.tar.gz
RUN tar -xvzf sass.tar.gz
ENV PATH="/dart-sass:${PATH}"

# install RVM, Ruby, and Bundler
#RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
#RUN curl -sSL https://get.rvm.io | bash -s stable
#RUN \curl -L https://get.rvm.io | bash -s stable version "1.9.3"
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN curl -sSL https://get.rvm.io | bash -s stable --rails
RUN /bin/bash -l -c "rvm requirements"
RUN /bin/bash -l -c "rvm install 2.4.2"
RUN /bin/bash -l -c "rvm use 2.4.2"
RUN /bin/bash -l -c "gem install bundler --no-ri --no-rdoc"

CMD ["bash"]
