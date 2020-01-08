FROM tansoft/openresty-php:latest

RUN apk add make git npm;\
        npm install -g \
        babel-cli cordova \
        eslint express http-proxy \
        less moment mysql nodemon \
        react redis request sass vue webpack

CMD ["sh","/usr/local/start.sh"]
