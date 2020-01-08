
# stage 1
From node:12.13.0 as node
RUN mkdir /usr/app
WORKDIR /usr/app
COPY . /usr/app
#means weare currently in angular source code this copy command will copy all source to docker image that we are building
RUN npm install
RUN npm install -g @angular/cli@8.3.17
RUN ng build --prod

# stage 2
FROM nginx:alpine
COPY --from=node /usr/app/dist/allmvr-client-website /usr/share/nginx/html
