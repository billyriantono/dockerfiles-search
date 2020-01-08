FROM node:6-alpine
ENV NODE_ENV production
# Note this is for local testing only -> ENV SQLAZURECONNSTR_MS_TableConnectionString Data Source=tcp:{azure db server}.database.windows.net,1433;Initial Catalog={db name};User ID={usr};Password={pwd}
WORKDIR /usr/src/appd
COPY ["package.json", "npm-shrinkwrap.json*", "./"]
# Note this is not required for non SQLite -> RUN npm install sqlite3
RUN npm install --production --silent && mv node_modules ../
COPY . .
EXPOSE 3000
CMD node app.js