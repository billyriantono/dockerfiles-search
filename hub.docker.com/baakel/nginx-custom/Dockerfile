FROM nginx:1.15.0-alpine

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 443
EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
