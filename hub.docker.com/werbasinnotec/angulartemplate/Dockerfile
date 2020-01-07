FROM mhart/alpine-node:5.1.0
MAINTAINER WERBAS Innotec <info@werbas-ag.com>

RUN apk update && \
    apk add \
      git \
      openssh \
      make \
      python && \
    \
    npm install -g \
      browserify \
      babel \
      babel-cli \
      gulp

RUN apk --no-cache add nginx

COPY nginx.conf /etc/nginx

WORKDIR /usr/share/site

COPY . /usr/share/site/
RUN npm install

CMD ["gulp", "public"]

CMD ["nginx", "-g", "daemon off;"]

EXPOSE 80
