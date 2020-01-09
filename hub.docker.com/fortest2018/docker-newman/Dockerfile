FROM node:alpine
ENV NEWMAN_VERSION 4.1.0

RUN npm install -g newman@${NEWMAN_VERSION};
RUN npm install -g newman-reporter-html;

WORKDIR /etc/newman
CMD ["newman"]
