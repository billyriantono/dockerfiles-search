FROM nginx:1.13.6-alpine
WORKDIR /var/www/neetshin

RUN apk -U upgrade \
 && apk add \
    git \
    nodejs \
 && npm install -g yarn \
 && rm -rf /var/cache/apk/* \
 && rm -f /etc/nginx/conf.d/default.conf

COPY yarn.lock package.json /var/www/neetshin/
COPY ./etc/neetshin.conf /etc/nginx/conf.d/

RUN yarn cache clean \
 && yarn --ignore-optional --pure-lockfile

COPY . /var/www/neetshin/

VOLUME /var/www/neetshin

EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
