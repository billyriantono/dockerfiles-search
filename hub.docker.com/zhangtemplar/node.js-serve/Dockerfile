FROM node
MAINTAINER zhangtemplar

# Prepare app directory
RUN mkdir -p /usr/src/app
ADD . /usr/src/app

# Install dependencies
WORKDIR /usr/src/app
RUN npm install
RUN npm install -g serve

# Expose the app port
EXPOSE 80

# Start the app
CMD serve  -p 80 -s build
