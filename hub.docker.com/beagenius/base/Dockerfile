FROM launcher.gcr.io/google/nodejs
RUN npm i npm@6.1.0 -g
RUN npm install -g spa-http-server
RUN npm install -g --no-optional @angular/cli@6.0.8
RUN npm install -g @angular-devkit/build-angular
RUN npm install pm2 -g
RUN apt-get update
RUN apt-get install build-essential
RUN apt-get install unzip
RUN apt-get -y install rsync
RUN apt-get -y install nano
RUN apt-get install wget
RUN wget https://github.com/emcrisostomo/fswatch/releases/download/1.11.3/fswatch-1.11.3.tar.gz
RUN tar -xvzf fswatch-1.11.3.tar.gz
RUN cd /app/fswatch-1.11.3 && ./configure && make && make install && ldconfig
RUN rm -r /app/fswatch-1.11.3*
RUN mkdir /server
RUN echo "cd /server"