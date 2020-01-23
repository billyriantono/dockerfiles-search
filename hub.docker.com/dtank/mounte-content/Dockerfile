# Pull base image.
FROM dspfac/devbox-web

#cordova, ionic and grunt
RUN npm install -g cordova@4.3.0
RUN npm install -g ionic@1.4.3
RUN npm install -g grunt-cli@0.1.13
RUN npm install -g grunt-contrib-watch@0.6.1
RUN npm install -g grunt-contrib-connect@0.10.1

ENV COURSE mobile-angular-react

EXPOSE 3005 8000 9000 35730 4000

ENV DISCOVER api-server:3005,user-server:8000,grunt-server:9000,livereload:35730,codebox-server:4000

WORKDIR /var/tmp

COPY . /root/

CMD /root/run.sh

