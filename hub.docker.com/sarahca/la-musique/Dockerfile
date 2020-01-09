FROM ubuntu
MAINTAINER sarahca

RUN apt-get update
RUN apt-get install -y nodejs git npm ruby ruby-sass
RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN mkdir /app

RUN cd /app && git clone https://github.com/sarahca/La-Musique.git
RUN cd /app/La-Musique && git checkout sarah_dev2

RUN cd /app/La-Musique && npm install

RUN cd /app/La-Musique && npm install -g bower grunt-cli
RUN cd /app/La-Musique && bower --allow-root install

RUN apt-get install -y 
env PATH /sbin:/usr/sbin:/bin:/usr/bin:/usr/local/bin
CMD ["/bin/sh", "-c", "cd /app/La-Musique && grunt serve:dist --force"]


