FROM nginx:alpine

WORKDIR /app

COPY . .

RUN cp nginx.conf /etc/nginx/nginx.conf

EXPOSE 443

CMD ["nginx", "-c", "./nginx.conf", "-g", "daemon off;"]
