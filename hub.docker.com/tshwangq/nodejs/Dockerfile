FROM google/nodejs
RUN npm config set registry https://registry.npm.taobao.org
WORKDIR /app
ONBUILD ADD package.json /app/
ONBUILD RUN npm install
ONBUILD ADD . /app

EXPOSE 8080
CMD []
ENTRYPOINT ["/nodejs/bin/npm", "start"]
