FROM ubuntu:14.04
MAINTAINER Tyler Griesbach <tgriesbach@tekniq.com>

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Add the ondrej php repo
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu trusty main" > /etc/apt/sources.list.d/ondrej-php-trusty.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C

RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y -q install php7.1 php7.1-gd php7.1-apcu \
    php7.1-sqlite php7.1-pgsql php-pear php7.1-mysql php7.1-intl php7.1-simplexml php7.1-sybase php7.1-geoip php7.1-gmp \
    php7.1-readline php7.1-mcrypt php7.1-xmlrpc php7.1-json php7.1-curl php7.1-soap php7.1-zip php7.1-mbstring php7.1-bcmath \
    php-apcu-bc rubygems-integration openssh-client wget curl exim4 libxrender1 gsfonts libssl-dev supervisor

# Run the node script that adds the repo automatically
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN apt-get -y update && apt-get -y -q install nodejs

# Install SASS using ruby gems
RUN gem install sass

# Install YARN
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y -q install yarn

# Configure Exim4, our SMTP server
RUN rm -rf /etc/exim4 && mkdir -p /etc/exim4
ADD exim4.conf /etc/exim4/exim4.conf

VOLUME ["/hosting_files"]

EXPOSE 9000
EXPOSE 25

ADD run.sh /start
RUN chmod +x /start

ENTRYPOINT ["/start"]