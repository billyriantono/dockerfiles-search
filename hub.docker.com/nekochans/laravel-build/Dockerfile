FROM amazonlinux:2.0.20190228

ENV TZ=Asia/Tokyo

RUN set -x && \
  yum update && \
  yum install -y git && \
  yum install -y aws-cli && \
  yum install -y zip unzip && \
  amazon-linux-extras install php7.3 -y && \
  yum install -y php php-opcache php-devel php-opcache php-mbstring php-xml && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  composer global require hirak/prestissimo && \
  yum install -y gcc-c++ make && \
  curl --silent --location https://rpm.nodesource.com/setup_10.x | bash - && \
  yum install -y nodejs && \
  npm install -g npm && \
  npm install -g yarn && \
  mkdir -p /app

COPY ./config/php.ini /etc/php.ini

WORKDIR /app
