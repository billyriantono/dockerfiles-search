FROM node:boron

# Create app directory
RUN mkdir -p /usr/src/turisalus-backend
WORKDIR /usr/src/turisalus-backend

# Install app dependencies and bundle app source
COPY . /usr/src/turisalus-backend

EXPOSE 8000

RUN npm install

CMD [ "npm", "start" ]