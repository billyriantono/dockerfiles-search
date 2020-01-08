FROM mhart/alpine-node
WORKDIR /usr/src/app
ADD ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
COPY . .
EXPOSE 3000
RUN npm i
CMD npm start

