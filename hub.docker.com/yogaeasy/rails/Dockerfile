FROM nishidayuya/docker-vagrant-debian:8.9

ENV DEBIAN_FRONTEND noninteractive
ENV RAILS_ENV staging
ENV RUBY_VERSION 2.5.1
ENV SA apt-get -qq -o=Dpkg::Use-Pty=0 -y

RUN sed -i 's/deb.debian.org/ftp2.de.debian.org/g' /etc/apt/sources.list \
 && $SA update \
 && $SA install git curl wget libmysqld-dev imagemagick libmagickwand-dev locales \
    apt-transport-https gnupg2 software-properties-common \
 && $SA install dirmngr gnupg memcached \
 && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
 && dpkg-reconfigure --frontend=noninteractive locales \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5072E1F5 \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 39499BDB \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4A9406876FCBD3C456770C88C718D3B5072E1F5 \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7D2BAF1CF37B13E2069D6956105BD0E739499BDB \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 561F9B9CAC40B2F7 \
 && $SA install ca-certificates \
 && echo 'deb https://oss-binaries.phusionpassenger.com/apt/passenger jessie main' > /etc/apt/sources.list.d/passenger.list \
 && $SA update \
 && $SA install nginx-extras passenger xvfb firefox-esr solr-jetty libmysqlclient-dev \
 && rm -rf /var/lib/apt/lists/* \
 && sed -i 's/# include \/etc\/nginx\/passenger.conf;/include \/etc\/nginx\/passenger.conf;/g' /etc/nginx/nginx.conf \
 && echo "\n\
 server { \n\
     listen 80;\n\
     server_name _;\n\
     # Tell Nginx and Passenger where your app's 'public' directory is\n\
     root /vagrant/public;\n\
     # Turn on Passenger\n\
     passenger_enabled on;\n\
     passenger_ruby /home/vagrant/.rvm/gems/ruby-${RUBY_VERSION}/wrappers/ruby;\n\
     passenger_app_env ${RAILS_ENV};\n\
     passenger_sticky_sessions on;\n\
     passenger_sticky_sessions_cookie_name _pr;\n\
     passenger_min_instances 1;\n\
 }" >/etc/nginx/sites-available/default \
 && ssh-keygen -A \
 && mkdir /vagrant \
 && chown vagrant.vagrant /vagrant \
 && curl -sSL https://rvm.io/mpapis.asc | gpg --batch --import - \
 && echo 409B6B1796C275462A1703113804BB82D39DC0E3:6: | gpg --batch --import-ownertrust \
 && curl -sSL https://rvm.io/pkuczynski.asc | gpg --batch --import - \
 && echo 7D2BAF1CF37B13E2069D6956105BD0E739499BDB:6: | gpg --batch --import-ownertrust \
 && echo "\n\
 cd /vagrant \n\
 gpg2 --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB \n\
 curl -sSL https://get.rvm.io | bash -s stable \n\
 echo 'source /home/vagrant/.rvm/scripts/rvm' >> /home/vagrant/.bashrc \n\
 source /home/vagrant/.rvm/scripts/rvm \n\
 rvm install "ruby-${RUBY_VERSION}" \n\
 gem install bundler \n\
 bundle config git.allow_insecure true" | sudo -u vagrant bash

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
