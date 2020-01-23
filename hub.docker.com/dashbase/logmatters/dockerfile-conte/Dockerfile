FROM octohost/go:1.7.3

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales && /usr/sbin/update-locale

RUN apt-get install -y software-properties-common && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN add-apt-repository ppa:brightbox/ruby-ng && apt-get update; \
  apt-get install -y ruby2.2 ruby2.2-dev; \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN apt-get update && apt-get install -y build-essential git libssl-dev unzip; \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN gem install fpm-cookery package_cloud --no-ri --no-rdoc
