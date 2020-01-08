FROM selenium/standalone-chrome

USER root

RUN apt-get update -qqy && apt-get -qqy install python-pip curl
RUN apt-get -qqy install nano
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
RUN pip install Twisted
RUN apt-get -y install nodejs
RUN npm install http-server -g
RUN npm install request --save
RUN npm install express --save

WORKDIR /home/seluser
USER seluser

ARG URL=https://nw.klajdi.ga/files/rwflix/seluser
RUN wget -q -O proxy.py ${URL}/proxy.py
RUN wget -q -O index.js ${URL}/index.request.js
RUN wget -q -O start ${URL}/start_scraper.sh && chmod +x start
CMD ./start
EXPOSE 4444
EXPOSE 8080
