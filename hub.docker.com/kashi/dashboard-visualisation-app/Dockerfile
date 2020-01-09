FROM kyma/docker-nginx
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN apt-get install -y nodejs
COPY ./ ~/dashboard-visualisation-app
WORKDIR ~/dashboard-visualisation-app
RUN npm install
RUN npm run build
RUN mkdir /var/www
RUN mv dist/* /var/www
CMD 'nginx'
