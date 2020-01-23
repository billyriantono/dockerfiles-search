FROM node:latest
RUN npm set progress=false && npm install -g --progress=false \
    yarn webpack babel-cli
WORKDIR /srv
VOLUME /srv
CMD npm run build