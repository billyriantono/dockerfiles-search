from node
RUN npm install -y express --save
RUN npm install body-parser --save
copy data.json /node/data.json
copy node.js /node/node.js
run chmod +x /node/node.js
expose 9000
cmd node /node/node.js
