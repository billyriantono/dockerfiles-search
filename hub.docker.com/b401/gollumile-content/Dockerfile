FROM node:10.16.2-alpine
LABEL maintainer="azucena.rosales@gmail.com"
RUN npm install -g create-react-app \
                   create-react-native-app \
                   react-native-cli
RUN mkdir -p /var/www/sites
WORKDIR /var/www/sites
ADD . /var/www/sites
CMD ["/bin/sh"]
