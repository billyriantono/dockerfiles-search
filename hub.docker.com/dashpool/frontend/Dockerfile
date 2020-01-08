

#"build-stage", build web app with nodejs
FROM  node:10 as build-stage


COPY ./package.json /app/
WORKDIR /app
RUN npm install --quiet
ENV PATH /usr/src/app/node_modules/.bin:$PATH
COPY . /app

RUN npm run dockerBuild




#Create Nginx web server 
FROM nginx:stable-alpine

COPY startup.sh /
RUN chmod 700 /startup.sh && dos2unix /startup.sh
COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 443
CMD ["/bin/sh", "/startup.sh"]