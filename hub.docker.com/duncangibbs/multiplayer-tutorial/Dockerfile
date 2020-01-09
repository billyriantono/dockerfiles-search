# build environment
FROM nikolaik/python-nodejs:latest
WORKDIR /
ENV PATH /node_modules/.bin:$PATH
COPY package.json /package.json
RUN npm install
COPY . /

EXPOSE 80

CMD ["npm", "start"]