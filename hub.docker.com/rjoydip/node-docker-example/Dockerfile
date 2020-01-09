FROM node:7
WORKDIR /
COPY . /src
COPY package.json /src/package.json
RUN cd /src; npm install --production
CMD ["node", "/src/index.js"]
EXPOSE 3000