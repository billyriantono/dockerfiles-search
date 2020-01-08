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

RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y -q install php7.0 php7.0-fpm php7.0-gd php7.0-apcu \
    php7.0-sqlite php7.0-pgsql php-pear php7.0-mysql php7.0-intl php7.0-simplexml php7.0-sybase php7.0-geoip php7.0-gmp \
    php7.0-readline php7.0-mcrypt php7.0-xmlrpc php7.0-json php7.0-curl php7.0-soap php7.0-zip php7.0-mbstring php7.0-bcmath \
    rubygems-integration openssh-client wget curl exim4 libxrender1 gsfonts libssl-dev supervisor

# Run the node script that adds the repo automatically
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN apt-get -y update && apt-get -y -q install nodejs

# Install YARN
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y -q install yarn


RUN wget http://tek-lin-devop.tekniq.com/wkhtmltopdf-0.11.0_rc1-static-amd64.tar.bz2
RUN tar xvjf wkhtmltopdf-0.11.0_rc1-static-amd64.tar.bz2
RUN install wkhtmltopdf-amd64 /usr/bin/wkhtmltopdf
RUN install wkhtmltopdf-amd64 /usr/local/bin/wkhtmltopdf

RUN gem install sass

# Configure Exim4, our SMTP server
RUN rm -rf /etc/exim4 && mkdir -p /etc/exim4
ADD exim4.conf /etc/exim4/exim4.conf

VOLUME ["/hosting_files"]

EXPOSE 9000
EXPOSE 25

# Copy supervisor config over
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

ADD run.sh /start
RUN chmod +x /start

ENTRYPOINT ["/start"]