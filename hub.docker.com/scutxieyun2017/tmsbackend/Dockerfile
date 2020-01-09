FROM node:10.16.3
RUN mkdir -p /home/Service
WORKDIR /home/Service
COPY bin bin
COPY public public
COPY views views
COPY package.json package.json
COPY package-lock.json package-lock.json
RUN npm install
#对app.js进行版本更新，来触发后续的cache失效
ADD app.js app.js
COPY modules modules
COPY routes routes
ENTRYPOINT [ "npm", "start" ]
##
