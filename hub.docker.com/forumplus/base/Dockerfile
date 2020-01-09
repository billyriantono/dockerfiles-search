FROM debian:9

ENV LANG=C.UTF-8

LABEL maintainer="Jan Schlosser <jan.schlosser@verdi-forum.de>"

RUN \
       DEBIAN_FRONTEND=noninteractive apt-get -qqy update \
    && DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
                                                   build-essential \
                                                   curl

RUN \
       curl -sL https://deb.nodesource.com/setup_11.x | bash - \
    && curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | DEBIAN_FRONTEND=noninteractive apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && DEBIAN_FRONTEND=noninteractive apt-get -qqy update

RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
                                                autoconf \
                                                automake \
                                                fop \
                                                git \
                                                imagemagick \
                                                inotify-tools \
                                                libgl1-mesa-dev \
                                                libglu1-mesa-dev \
                                                libncurses5-dev \
                                                libpng-dev \
                                                libssl-dev \
                                                libwxgtk3.0-dev \
                                                libxml2-utils \
                                                netcat-traditional \
                                                postgresql-client \
                                                procps \
                                                unixodbc-dev \
                                                unzip \
                                                xsltproc \
                                                yarn

RUN \
     mkdir -p /opt/app /var/www \
  && chown www-data:www-data /opt/app /var/www

ADD --chown=www-data:www-data .tool-versions /opt/app/
ADD --chown=www-data:www-data prepare-asdf-elixir /var/www/

USER www-data:www-data
WORKDIR /opt/app
RUN /var/www/prepare-asdf-elixir
USER root:root
