FROM node:latest
RUN npm install -g @oracle/ojet-cli
RUN mkdir -p /usr/src/SAM
WORKDIR /usr/src/SAM
COPY . /usr/src/SAM
RUN npm install
EXPOSE 8000
CMD ojet serve
