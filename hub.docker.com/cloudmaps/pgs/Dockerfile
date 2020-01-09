FROM alexd1971/debian-node:6
RUN apt-get update
RUN apt-get install -y git python build-essential
RUN mkdir /pgs
COPY . /pgs/
WORKDIR /pgs/
RUN npm install
RUN npm install -g bower grunt
RUN echo '{ "allow_root": true }' > /root/.bowerrc
RUN bower install
RUN grunt bower:install
RUN npm uninstall -g bower grunt
RUN rm -rf bower_components
RUN apt-get purge -y git python build-essential
RUN apt-get autoremove -y
CMD ./node_modules/sails/bin/sails.js lift --prod
EXPOSE 1337