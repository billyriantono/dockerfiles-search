from node:10
workdir /usr/src/app
copy package*.json ./
copy . .
run ["npm", "install"]
expose 80
cmd ["node", "app.js"]
