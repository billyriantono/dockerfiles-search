
FROM selenium/standalone-firefox:latest

MAINTAINER Harley Bussell <harley_bussell@flightcentre.com.au>

# Install node packages.
COPY ./src/package.json /var/node-install/package.json
COPY ./src/.npmrc /var/node-install/.npmrc
COPY ./src/install.sh /var/install.sh
COPY ./src/fetch-db.php /var/fetch-db.php

RUN echo "Installing ..."
RUN sudo /var/install.sh

RUN echo "Fetch db ..."
RUN php /var/fetch-db.php


