# Pull base image.
FROM dspfac/codebox-fix

ENV NPM_CONFIG_LOGLEVEL warn

RUN npm install -g react-native@0.12

ENV COURSE react-native

EXPOSE 3005 8081 4000

VOLUME /var/tmp

ENV DISCOVER api-server:3005,user-server:8081,codebox-server:4000

WORKDIR /var/tmp

COPY . /root/

CMD /root/run.sh
