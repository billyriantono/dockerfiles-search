from node
label maintainer dj@dwvops-rest.com
RUN npm install -y express --save
RUN npm install -y  body-parser --save
COPY node.js /nodeserver/node.js
COPY data.json /nodeserver/data.json
run chmod =X /nodeserver/node.js
EXPOSE 9000
workdir /nodeserver
cmd node /nodeserver/node.js
