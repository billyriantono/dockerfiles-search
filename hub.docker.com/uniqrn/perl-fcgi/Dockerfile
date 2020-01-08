FROM httpd:latest
LABEL maintainer "unicorn research Ltd"

RUN apt-get update && apt-get install -y --no-install-recommends wget make gcc git

WORKDIR /opt
RUN wget http://ftp.riken.jp/net/apache/httpd/mod_fcgid/mod_fcgid-2.3.9.tar.gz \
  && tar xzf mod_fcgid-2.3.9.tar.gz

WORKDIR /opt/mod_fcgid-2.3.9
RUN . ./configure.apxs \
  && make && make install \
  && yes '' | cpan -i CGI::Fast \
  && yes '' | cpan -i LWP::Simple

RUN apt-get purge -y --auto-remove make gcc

COPY httpd.conf /usr/local/apache2/conf/
COPY httpd-fcgi.conf /usr/local/apache2/conf/extra/
