FROM debian:jessie
MAINTAINER Kimura Youichi <yoichi.kimura@tejimaya.com>

RUN apt-get update && \
  apt-get install -y --no-install-recommends apache2 libapache2-mod-fcgid && \
  apt-get clean && rm -r /var/lib/apt/lists/*

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends mysql-server && \
  apt-get clean && rm -r /var/lib/apt/lists/*

RUN apt-get update && \
  apt-get install -y --no-install-recommends php5 php5-cgi php5-mysql php5-mcrypt php5-apcu ttf-bitstream-vera php5-gd && \
  apt-get clean && rm -r /var/lib/apt/lists/*

RUN apt-get update && \
  apt-get install -y --no-install-recommends locales && \
  echo 'ja_JP.UTF-8 UTF-8' > /etc/locale.gen && locale-gen && update-locale LANG=ja_JP.UTF-8 && \
  apt-get clean && rm -r /var/lib/apt/lists/*

ADD apache.conf /etc/apache2/conf-available/local.conf

RUN a2enmod vhost_alias rewrite headers fcgid && a2enconf local

RUN echo "Asia/Tokyo" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
