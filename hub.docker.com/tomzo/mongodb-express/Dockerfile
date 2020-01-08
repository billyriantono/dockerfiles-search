FROM irakli/node-alpine:5.11-runit

EXPOSE 8081

# override some config defaults with values that will work better for docker
ENV ME_CONFIG_MONGODB_SERVER="mongo"
ENV ME_CONFIG_MONGODB_ENABLE_ADMIN="true"
ENV VCAP_APP_HOST="0.0.0.0"

WORKDIR /app

COPY mongo-express/ /app

RUN cp config.default.js config.js

RUN npm install

COPY runit /etc/service/node-app
RUN chmod -R 755 /etc/service/node-app

CMD ["/sbin/runit_init"]
