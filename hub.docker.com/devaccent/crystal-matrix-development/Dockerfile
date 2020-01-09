FROM devaccent/crystal-matrix-base:latest

MAINTAINER "Alexandru Berce" <alex@devaccent.com>

# Install Xdebug
RUN yum -y install php72w-pecl-xdebug

# Install go
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH

# Configure mailhog
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/local/bin/mhsendmail
COPY config/mailhog.ini /etc/php.d/

# Install xdebug
COPY config/xdebug.ini /etc/php.d/