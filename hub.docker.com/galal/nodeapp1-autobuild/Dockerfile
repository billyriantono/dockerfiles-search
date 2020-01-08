FROM node
LABEL maintainer="galal.elatfawy@gmail.com"
WORKDIR /src
COPY package.json .
RUN npm install
COPY . /src
EXPOSE 5000
EXPOSE 5002
CMD npm start
