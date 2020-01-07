FROM jkarkoszka/apache-php-java
MAINTAINER Jakub Karkoszka <karkoszka@gmail.com>

RUN apt-get update && \
  apt-get -y install \
    build-essential \
	software-properties-common \
	python-software-properties \
	libav-tools \
	libgif-dev \
	xpdf \
	libfreetype6 \
	libfreetype6-dev \
	libjpeg62 \
    && \
  apt-get clean && \
  cd /usr/local/src && \
  wget http://www.swftools.org/swftools-0.9.1.tar.gz && \
  tar -vxf swftools-0.9.1.tar.gz && \
  cd /usr/local/src/swftools-0.9.1/lib/pdf \
  wget ftp://ftp.foolabs.com/pub/xpdf/xpdf-3.04.tar.gz && \
  cd /usr/local/src/swftools-0.9.1 && \
  sh ./configure && \
  cd /usr/local/src/swftools-0.9.1  && \
  make && \
  make install

COPY ./configure.sh /
RUN ["chmod", "+x", "/configure.sh"]

EXPOSE 80

ENTRYPOINT ["/configure.sh"]
