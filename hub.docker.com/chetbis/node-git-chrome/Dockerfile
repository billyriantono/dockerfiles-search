FROM debian:stable-slim

RUN apt-get update
RUN apt-get install -yy wget curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash - && \
	apt-get update && apt-get install -y nodejs && \
  npm i -g npm@6

LABEL maintainer "Bishnu Chetia <chetiabishnu95@gmail.com>"

RUN node -v && npm -v

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable xvfb

# install git and slim down image
RUN apt-get -y update && apt-get -y install git && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/man/?? /usr/share/man/??_*

RUN git --version
RUN npm -v
RUN apt update && apt install -y procps
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*
