FROM 5t111111/node:v0.10.31

MAINTAINER 5t111111 https://github.com/5t111111

RUN apt-get update -qq
RUN apt-get install -y -qq supervisor
RUN apt-get clean

RUN adduser --gecos 'jsDAV' --disabled-password jsdav

WORKDIR /home/jsdav/app

ADD assets/package.json /home/jsdav/app/
ADD assets/server.js /home/jsdav/app/
ADD assets/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN mkdir data

RUN npm install

RUN chown -R jsdav:jsdav ./

EXPOSE 8000

CMD ["/usr/bin/supervisord"]
