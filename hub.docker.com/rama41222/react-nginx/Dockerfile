FROM nginx:1.15.7-alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf

RUN nginx -t

CMD ["nginx", "-s", "reload"]
