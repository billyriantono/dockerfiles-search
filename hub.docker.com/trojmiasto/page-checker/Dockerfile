FROM node:6.11

LABEL maintainer="Łukasz Górski <l.gorski@trojmiasto.pl>"

RUN apt-get update \
  && apt-get install -y \
    libgtk2.0-0 \
    libgconf-2-4 \
    libasound2 \
    libxtst6 \
    libxss1 \
    libxss1 \
    libnss3 \
    xvfb

RUN git clone https://bitbucket.org/ri0ter/page-checker /opt/page-checker

WORKDIR /opt/page-checker

RUN npm install

EXPOSE 8080

# default server port 8080, to change add at the end: -- -p <port>
CMD xvfb-run --server-args="-screen 0 1024x768x24" npm run server
