# Debian wheezy with PHP 5.5 installed via dotdeb
# Also includes php5-mysql and php5-mcrypt.  
# Intended for cns

FROM debian:wheezy

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install gnupg wget apt-utils -y && wget https://www.dotdeb.org/dotdeb.gpg --no-check-certificate && apt-key add dotdeb.gpg

RUN echo "deb http://packages.dotdeb.org wheezy-php55 all" >> /etc/apt/sources.list.d/dotdeb.list && \
    echo "deb-src http://packages.dotdeb.org wheezy-php55 all" >> /etc/apt/sources.list.d/dotdeb.list 

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install php5 php5-mysql php5-mcrypt -y