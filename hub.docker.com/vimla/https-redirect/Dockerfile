FROM nginx:1.14-alpine

COPY default.conf /etc/nginx/conf.d/default.conf

RUN sed -i 's/sendfile.*on\;/sendfile off\;/' /etc/nginx/nginx.conf

CMD ["nginx", "-g", "daemon off;"]
