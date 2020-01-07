FROM node:alpine
RUN mkdir -p /var/www/html/themes/custom/theme
RUN touch /var/www/html/themes/custom/theme/gulpfile.js
COPY package.json /var/www/html/themes/custom/theme/package.json
RUN npm install -g gulp
RUN cd /var/www/html/themes/custom/theme && npm install && npm link gulp
EXPOSE 80

