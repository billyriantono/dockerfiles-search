# FROM node
# WORKDIR /usr/src/app
# COPY package*.json /usr/src/app/
# RUN npm install
# COPY . /usr/src/app
# EXPOSE 3000
# EXPOSE 27017
# CMD [ "npm", "start" ]

FROM node
WORKDIR /app
ADD . /app
RUN npm install
EXPOSE 3000
EXPOSE 27017
CMD [ "npm", "start" ]
