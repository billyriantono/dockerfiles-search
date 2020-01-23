FROM node:alpine
ADD . /tdmoc.com/
WORKDIR /tdmoc.com/
RUN npm install
RUN npm install -g supervisor browserify uglifycss
RUN npm install -G envify
CMD ["npm","run","build"]
