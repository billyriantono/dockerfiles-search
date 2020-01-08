FROM node:alpine
ADD . /ushuaiaking.com.ar/
WORKDIR /ushuaiaking.com.ar/
RUN npm install
RUN npm install -g supervisor browserify uglifycss
RUN npm install -G envify
CMD ["npm","run","build"]
