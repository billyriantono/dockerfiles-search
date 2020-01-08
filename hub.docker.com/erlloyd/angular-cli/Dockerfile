FROM node:6.9.5
MAINTAINER Eric Lloyd

#add yarn to apt-get
RUN apt-get update && apt-get install apt-transport-https 
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && apt-get install yarn=0.23.3-1

RUN npm install -g @angular/cli@1.0.1

EXPOSE 4200