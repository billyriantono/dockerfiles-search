# Pull base image.
FROM dspfac/codebox-fix

ENV NPM_CONFIG_LOGLEVEL warn

#install other npm dependencies
RUN npm install -g mocha@2.1.0
RUN npm install -g grunt-cli@0.1.13
RUN npm install -g http-server@0.7.4

# course specific npms
# for nodejs-stream-adventure validation
RUN npm install -g stream-adventure@4.0.2
RUN npm install -g through2
RUN npm install -g split
RUN npm install -g concat-stream
RUN npm install -g request
RUN npm install -g stream-combiner
RUN npm install -g trumpet
RUN npm install -g websocket-stream
RUN npm install -g duplexer2
RUN npm install -g stream-combiner
RUN npm install -g strip
RUN npm install -g crypto
RUN npm install -g tar

# course specific npms
# for nodejs-learn-you-node course validation
RUN npm install -g learnyounode@2.5.0
RUN npm install -g strip-ansi@2.0.1
RUN npm install -g path
RUN npm install -g bl
RUN npm install -g through2-map

# course specific npms
# for javascripting course validation
RUN npm install -g javascripting@1.12.0

ENV COURSE js

EXPOSE 3005 8000 4000

VOLUME /var/tmp

ENV DISCOVER api-server:3005,user-server:8000,codebox-server:4000

WORKDIR /var/tmp

COPY . /root/

CMD /root/run.sh
