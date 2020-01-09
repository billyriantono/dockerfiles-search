FROM node:10.15-alpine
ENV NODE_ENV production
ENV TEST_FILE=test.js
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --production --silent && mv node_modules ../
COPY . .
# add www.google.com/images
RUN node ${TEST_FILE}
EXPOSE 8080
# ENTRYPOINT [ "" ]
CMD npm start