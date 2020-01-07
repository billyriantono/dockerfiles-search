FROM node:7

MAINTAINER Marcus Vinicius Cardoso <dev@mviniciusconsultoria.com.br>

RUN useradd --user-group --create-home --shell /bin/false app

ENV DISPLAY :99
ENV CHROME_BIN /usr/bin/chromium

# Commands for instalation
RUN apt-get update && \
  apt-get install -y --force-yes xvfb chromium libgconf-2-4 && \
  apt-get autoremove -y && \
  apt-get clean -y && \
  npm install --global @angular/cli@latest

# Entrypoint for tests
ADD entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
