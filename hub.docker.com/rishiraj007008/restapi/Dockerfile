from node
label maintainer rishiraj@oracle.com
RUN npm install -y express --save
RUN npm install -y body-parser --save
copy node.js /nodeserver/node.js
copy data.json /nodeserver/data.json
run chmod +x /nodeserver/node.js
EXPOSE 9000
workdir /nodeserver
cmd node /nodeserver/node.js
