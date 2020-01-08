# base image
FROM node:9.10.0

# set working directory
RUN mkdir /unison
RUN npm install -g create-react-app
RUN create-react-app /unison/my-app
VOLUME /unison/my-app
WORKDIR /unison/my-app
# start app
CMD ["npm", "start"]