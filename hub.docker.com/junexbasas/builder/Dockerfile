FROM node:alpine
RUN apk add git
RUN git clone https://github.com/antoniobasasjr/testsample.git
WORKDIR /home/node/testsample
RUN git config --global user.email "antoniobasasjr@gmail.com"
RUN git config --global user.name "antoniobasasjr"
RUN npm install
CMD node app.js