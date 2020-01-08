FROM node
ADD . /app
WORKDIR /app
RUN npm set strict-ssl false
RUN npm install
CMD node index.js