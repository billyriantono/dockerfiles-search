FROM nginx

LABEL maintainer="Brian McCarthy <brian.mcc@rthy.org>"

# need nodejs to be able to build and install packages on the container
RUN apt-get update && apt-get install -y curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash
RUN apt-get update && apt-get install -y nodejs 

# build application and copy to nginx html folder 
RUN mkdir -p /app
COPY . /app
WORKDIR /app
RUN npm install && npm cache clean && npm run build && cp -R dist/* /usr/share/nginx/html

# copy frontend.conf file to tell nginx to forward /api to correct container
COPY frontend.conf.template /etc/nginx/conf.d/frontend.conf.template

# run.sh replaces the api uri placeholder with the environment variable and starts nginx
COPY run.sh /run.sh
CMD ["/bin/sh", "/run.sh"]
