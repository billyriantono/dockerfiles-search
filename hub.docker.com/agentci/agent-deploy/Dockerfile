FROM node
MAINTAINER qazs

RUN mkdir /root/.ssh
RUN echo "Host bitbucket.org github.com\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config

ADD . /app
WORKDIR /app
RUN npm install
CMD ["npm", "start"]
