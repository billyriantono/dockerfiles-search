FROM verdaccio/verdaccio:3.11.6

RUN npm install --production --registry=https://registry.npm.taobao.org && npm i verdaccio-gitlab --registry=https://registry.npm.taobao.org

RUN ln -s /usr/local/app/node_modules/verdaccio-gitlab/build /verdaccio/plugins/verdaccio-gitlab

COPY ./config.yaml /verdaccio/conf/
