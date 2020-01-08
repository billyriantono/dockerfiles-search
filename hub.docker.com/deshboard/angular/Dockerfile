FROM sagikazarmark/dashboard:angular

RUN apt-get update && apt-get -y install nginx
COPY nginx.conf /etc/nginx/sites-available/default

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD ARG APP_ENV=prod
ONBUILD ENV APP_ENV $APP_ENV
ONBUILD COPY package.json /usr/src/app/
ONBUILD RUN npm install
ONBUILD COPY . /usr/src/app
ONBUILD RUN ng build --env=$APP_ENV

CMD ["nginx", "-g", "daemon off;"]

HEALTHCHECK --interval=1m --timeout=3s CMD curl -f http://localhost/__health || exit 1
