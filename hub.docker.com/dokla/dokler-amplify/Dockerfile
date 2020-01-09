FROM dokla/dokler-nodejs:latest

MAINTAINER Dokla Enterprise

RUN apt-get update

RUN npm install -g @aws-amplify/cli

RUN npx create-react-app myapp

RUN cd myapp && npm install @aws-amplify/api @aws-amplify/pubsub

WORKDIR /root/myapp

CMD ["npm", "start"]

EXPOSE 3000
