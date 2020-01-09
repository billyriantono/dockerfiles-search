FROM nginx:1.14.2
COPY conf.d/ /etc/nginx/conf.d/
COPY stream_conf.d/ /etc/nginx/stream_conf.d/
COPY nginx.conf /etc/nginx/nginx.conf
WORKDIR /etc/nginx/
CMD ["nginx", "-g", "daemon off;"]
