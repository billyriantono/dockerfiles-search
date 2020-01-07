FROM node:latest
RUN npm i -g http-server
ADD meegoportal/Seed-project /meego/portal
WORKDIR /meego/portal
RUN yarn 
RUN yarn build
WORKDIR /meego/portal/dist
CMD ["http-server", "-s", "-c-1"]