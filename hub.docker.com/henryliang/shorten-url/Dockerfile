FROM node:10
EXPOSE 3000
EXPOSE 5000

# update
RUN apt-get update

# copy the repo to app directory
RUN mkdir -p /usr/src/app
COPY . /usr/src/app

# prepare the client
WORKDIR /usr/src/app/client
RUN npm install

# prepare the app
WORKDIR /usr/src/app
RUN npm install

# run

ENTRYPOINT [ "/bin/bash", "-c", "./start.sh"] 
# /bin/bash -c /usr/src/app/start.sh
