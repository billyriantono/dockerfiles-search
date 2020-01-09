FROM node:alpine
ADD . /infoallinclusive.com/
WORKDIR /infoallinclusive.com/
RUN npm install
RUN npm install -g supervisor browserify uglifycss
RUN npm install -G envify
CMD ["npm","run","build"]
