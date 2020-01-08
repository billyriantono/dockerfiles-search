FROM ubuntu:16.04
MAINTAINER nrosu@pentalog.fr

#for compatibility problems with dmesg
ENV TERM=xterm-256color

RUN sed -i "s/http:\/\/archive./http:\/\/fr.archive./g" /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y \
    -o APT::Install-Recommend=false -o APT::Install-Suggests=false \
    apache2 vim

EXPOSE 80
EXPOSE 443

RUN apache2ctl -D FOREGROUND
#CMD ["apache2ctl", "-D", "FOREGROUND"]
