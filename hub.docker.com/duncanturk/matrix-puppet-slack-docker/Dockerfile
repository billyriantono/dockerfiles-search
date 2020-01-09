FROM node:11

# setup env
ENV APPDIR=/home/node/app/
ENV CONFDIR=/home/node/conf/

RUN mkdir $APPDIR && chown node:node $APPDIR
RUN mkdir $CONFDIR && chown node:node $CONFDIR
WORKDIR $APPDIR


# setup matrix-puttet-slack
RUN git clone https://github.com/matrix-hacks/matrix-puppet-slack.git $APPDIR && git checkout 4a18208a4b4f81a8ba311df2c7412f5155d8771b
RUN npm install


# do docker stuff
COPY run-docker.sh $APPDIR

USER node

EXPOSE 8090

VOLUME $CONFDIR

CMD $APPDIR/run-docker.sh
