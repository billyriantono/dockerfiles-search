FROM node:carbon as build
RUN chown -R node:node /usr/local/lib/node_modules
RUN chown -R node:node /usr/local/bin
USER node
RUN npm install -g @angular/cli
USER root
WORKDIR /Bookshelf.Angular
Copy . .
RUN npm install
RUN ng build

FROM nginx:1.12
COPY --from=build /Bookshelf.Angular/wwwroot /usr/share/nginx/html
EXPOSE 80

