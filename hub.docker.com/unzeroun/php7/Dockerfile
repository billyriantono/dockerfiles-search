FROM unzeroun/base

ENV DEBIAN_FRONTEND noninteractive

RUN wget https://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg

ADD dotdeb.list /etc/apt/sources.list.d/dotdeb.list

RUN aptitude update
RUN aptitude -y install php7.0 php7.0-cli php7.0-curl php7.0-opcache php7.0-dev php7.0-mysql php7.0-intl \
                        php7.0-gd php7.0-json php7.0-mbstring php7.0-pgsql

ADD php.ini /etc/php/7.0/cli/php.ini
