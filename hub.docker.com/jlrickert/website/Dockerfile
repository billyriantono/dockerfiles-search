FROM nginx:alpine
VOLUME /data
COPY nginx.conf /etc/nginx/nginx.conf
COPY . /app
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
