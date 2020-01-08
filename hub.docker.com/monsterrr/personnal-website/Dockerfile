FROM node:13.5.0-alpine

LABEL maintainer="Ludovic Ortega mastership@hotmail.fr"

# update package
RUN apk update

# copy program and requirements
COPY * /app/frontend/

# set workdir
WORKDIR /app/frontend/

# install dependencies
RUN npm install

# build frontend
RUN npm run-script build

# create static directory
RUN mkdir -p /opt/services/frontend/static/

# copy dist files in static directory
RUN mv ./dist/* /opt/services/frontend/static/
