FROM node:boron

# Install Kitewheel Web Client
RUN mkdir -p /usr/src/app
COPY . /usr/src/app
RUN rm -rf /usr/src/app/test
RUN rm -rf /usr/src/app/Dockerfile-development
WORKDIR /usr/src/app
RUN npm install --production --silent
RUN npm run build

RUN apt-get update &&\
    apt-get install -y libgtk2.0-0 libgconf-2-4 \
    libasound2 libxtst6 libxss1 libnss3 xvfb

EXPOSE 8888

CMD [ "bash", "./start.sh"]