FROM amazonlinux:2018.03.0.20180622

EXPOSE 80

# Set server timezone
RUN ln -f -s /usr/share/zoneinfo/America/New_York /etc/localtime

## Disabled reqs
# gcc \
# make \
# aws-cli \
# awslogs \
# python \
# vi \
# wget \

# PHP/Apache stack
RUN REQUIREMENTS="\
  aws-cli \
  git \
  cronie \
  httpd24 \
  mod24_ssl \
  mysql \
  openssl-devel \
  php71 \
  php71-gd \
  php71-devel \
  php71-intl \
  php71-mcrypt \
  php71-mysqlnd \
  php71-dba \
  php71-soap \
  php71-pdo \
  php71-opcache \
  php71-bcmath \
  php71-mbstring \
  php71-pecl-apcu \
  php71-pecl-memcached \
  php71-pecl-xdebug" \
  # Removes existing PHP/Apache stack
  && yum remove httpd* php* -y \
  # Installs new PHP/Apache stack
  && yum install $REQUIREMENTS -y \
  # Add crontab file
  && touch /var/spool/cron/root

# Install python pip
# RUN cd /tmp \
  # && wget https://bootstrap.pypa.io/get-pip.py \
  # && python get-pip.py \
  # && cd /

# Setup custom CloudWatch memory metrics scripts
# RUN pip install cloudwatchmon \
  # log memory metrics by instance
  # && echo "*/5 * * * * /usr/local/bin/mon-put-instance-stats.py --mem-util --mem-used --mem-avail --swap-util --swap-used --from-cron" >> /var/spool/cron/root \
  # log memory metrics by auto scaling group memory
  # && echo "*/5 * * * * /usr/local/bin/mon-put-instance-stats.py --mem-util --mem-used --mem-avail --swap-util --swap-used --auto-scaling=only --from-cron" >> /var/spool/cron/root \
  # log memory metrics by aggregation
  # && echo "*/5 * * * * /usr/local/bin/mon-put-instance-stats.py --mem-util --mem-used --mem-avail --swap-util --swap-used --aggregated=only --from-cron" >> /var/spool/cron/root

# Composer
RUN cd /tmp \
  && curl -sS https://getcomposer.org/installer | php \
  && chmod +x composer.phar \
  && mv composer.phar /usr/bin/composer \
  && cd /

# Node
# RUN cd /tmp \
  # && curl --silent --location https://rpm.nodesource.com/setup_6.x | bash \
  # && yum install -y nodejs-6.9.5 \
  # && npm install -g bower gulp \
  # && cd /

# Upgrade jmespath
# RUN mv /usr/bin/jp /usr/bin/jp-ami-version \
  # && cd /tmp \
  # && wget https://github.com/jmespath/jp/releases/download/0.1.2/jp-linux-amd64 \
  # && chmod +x ./jp-linux-amd64 \
  # && mv ./jp-linux-amd64 /usr/bin/jp \
  # && cd /

ADD cert/server.crt /var/www/ssl/localhost.crt
ADD cert/server.key /var/www/ssl/localhost.key
ADD php/php.ini /etc/php.d/zeel_php.ini
ADD php/xdebug.ini /etc/php.d/20-xdebug.ini
ADD sites.conf /etc/httpd/conf.d/sites-available.conf

# Pre setup httpd
RUN mkdir -p /var/www/logs \
  && mkdir -p /var/www/uploads \
  && mv /etc/httpd/conf.d/ssl.conf /etc/httpd/conf.d/ssl.conf_

RUN echo "* * * * * curl -k https://web/cron/all" >> /var/spool/cron/root \
  && service crond start

WORKDIR /var/www/html

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]