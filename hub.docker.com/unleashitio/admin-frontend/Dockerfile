# base image
FROM node:8.11.3

# set working directory
RUN mkdir /usr/src/app
WORKDIR /usr/src/app

# add `/usr/src/app/node_modules/.bin` to $PATH
ENV PATH /usr/src/app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /usr/src/app/package.json
CMD echo "Test1"
RUN npm install
CMD echo "Test2"
RUN npm install -g @angular/cli@7.0.4


# add app
COPY . /usr/src/app

# start app
CMD ng serve --host 0.0.0.0