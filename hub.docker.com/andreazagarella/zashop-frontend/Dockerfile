FROM node:latest as angularbuild
WORKDIR /app
ADD ZaShop ./
COPY nginx/default.conf ./nginx/default.conf
RUN rm -rf node_modules
RUN npm config set user 0
RUN npm config set unsafe-perm true
RUN npm install -g @angular/cli
RUN npm install
RUN ng build --prod
RUN mkdir ./nginx/html/  && cp -r ./dist/ZaShop ./nginx/html

FROM nginx:alpine
COPY --from=angularbuild /app/nginx/default.conf /etc/nginx/conf.d//default.conf
COPY --from=angularbuild /app/nginx/html/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
