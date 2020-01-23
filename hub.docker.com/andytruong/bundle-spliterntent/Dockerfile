FROM nginx:1.13.12-alpine
RUN apk update
RUN apk add dos2unix
RUN rm /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf
RUN dos2unix /etc/nginx/nginx.conf
# Run NGINX
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
