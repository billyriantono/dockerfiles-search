FROM nginx:latest
MAINTAINER Kyle Mathews "mathews.kyle@gmail.com"

RUN rm /etc/nginx/nginx.conf /etc/nginx/mime.types
COPY nginx.conf /etc/nginx/nginx.conf
COPY basic.conf /etc/nginx/basic.conf
COPY mime.types /etc/nginx/mime.types
RUN mkdir /etc/nginx/ssl
COPY default /etc/nginx/sites-enabled/default
COPY default-ssl /etc/nginx/sites-available/default-ssl
COPY directive-only /etc/nginx/directive-only
COPY location /etc/nginx/location

# expose both the HTTP (80) and HTTPS (443) ports
EXPOSE 80 443

# install some tools needed for most build steps
RUN apt-get update && apt-get install -y curl gnupg2 git build-essential && \
  curl -sL https://deb.nodesource.com/setup_9.x | bash - && \
  apt-get install -y nodejs && \
  npm install -g grunt-cli bower yo generator-karma generator-angular

CMD ["nginx"]

