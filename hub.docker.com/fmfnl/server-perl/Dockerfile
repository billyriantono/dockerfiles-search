FROM httpd:2.4.29
LABEL maintainer="Comcie <comcie@fmf.nl>"

RUN apt-get update && apt-get -y install \
    cpanminus \
    curl \
    libapache2-mod-perl2 \
    libdata-printer-perl \
    libdbd-mysql-perl \
    libdbi-perl \
    libfile-slurp-perl \
    libgetopt-long-descriptive-perl \
    libhtml-template-perl \
    libhttp-negotiate-perl \
    liblwp-useragent-determined-perl \
    libtest-strict-perl \
    libwww-mechanize-perl \
    libxml-libxml-perl \
    libxml-simple-perl \
    libxml-twig-perl

COPY httpd.conf /usr/local/apache2/conf/

RUN ln -s /usr/local/apache2/htdocs /fmf