#para ejecutar test e2e node se necesita la version jessie, no sirve la alpine
FROM node:8.15.0-jessie

#older versions https://www.slimjet.com/chrome/google-chrome-old-version.php

RUN apt-get update && apt-get install -qq -y \
    build-essential libpq-dev libffi-dev libnss3 libgconf-2-4 --no-install-recommends

ADD ./versions/76.0.3809.100/google-chrome-stable_current_amd64.deb google-chrome-stable_current_amd64.deb

#RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install

ENTRYPOINT ["sh", "-c", "ls"]
