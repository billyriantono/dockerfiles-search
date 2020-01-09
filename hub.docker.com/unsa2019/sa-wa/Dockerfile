# base image
FROM node:12.2.0-alpine

# set working directory
WORKDIR /app
# Install app dependencies

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /app/
RUN npm install
RUN npm install -g @vue/cli
RUN npm install axios
# Bundle app source
COPY . /app/


# start app
CMD ["npm", "run", "serve"]

