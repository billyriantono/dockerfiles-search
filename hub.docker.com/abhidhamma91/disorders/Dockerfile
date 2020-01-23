FROM nginx:1.14.2-alpine

COPY ./build /var/www/disorders.abhidhamma.com
COPY ./nginx.conf /etc/nginx/conf.d/disorders.abhidhamma.com.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]