FROM node:argon

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY . /usr/src/app

EXPOSE 8080

ENV EXTERNALURL "http://localhost:8080"

RUN chmod 755 ./bin/npm_lazy

CMD [ "sh", "-c", "node ./bin/npm_lazy --externalUrl $EXTERNALURL" ]
