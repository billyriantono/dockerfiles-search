#stage 1
FROM node:latest as node
WORKDIR /app
COPY package.json .
RUN npm cache clean --force
#RUN npm install http-server --g
RUN npm install -g @angular/cli@latest
RUN npm install
COPY . .
CMD npm start
#RUN npm run build --prod
#CMD ["http-server", "/app/dist/mdb-angular-pro"]
EXPOSE 4200
#stage 2
#FROM nginx:alpine
#COPY --from=node /app/dist/mdb-angular-pro /usr/share/nginx/html
