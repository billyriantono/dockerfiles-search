FROM httpd:2.4
COPY files/uniqueid /usr/local/apache2/cgi-bin
COPY files/index.html /usr/local/apache2/htdocs
COPY files/internal.css /usr/local/apache2/htdocs
COPY files/httpd.conf /usr/local/apache2/conf

RUN apt update
RUN apt install -y vim make gcc perl

RUN cpan CGI
RUN cpan App::cpanminus
RUN cpanm Text::Soundex