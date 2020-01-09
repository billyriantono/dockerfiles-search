FROM codefresh/buildpacks:all

ENV NVM_BIN /root/.nvm/versions/node/v0.12.7/bin
ENV PATH $NVM_BIN:$PATH

RUN npm install -g gulp

EXPOSE 9000
ENV PORT 9000

COPY package.json /src/package.json
WORKDIR /src
RUN npm install

COPY bower.json /src/bower.json
RUN bower install --allow-root --config.interactive=false

COPY . /src
RUN gulp build

CMD node app.js
