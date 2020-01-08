# base image
FROM node:12.2.0-alpine

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH node_modules/.bin:$PATH

# install and cache app dependencies
COPY . /app/

RUN npm install
RUN npm install --save axios vue-axios
RUN npm install vue


# start app
CMD ["npm", "run", "dev"]

EXPOSE 8080
