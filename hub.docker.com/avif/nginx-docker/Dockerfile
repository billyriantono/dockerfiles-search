FROM nginx:1.10

ADD nginx.conf /etc/nginx/nginx.conf
ADD start.sh /etc/nginx/start.sh

CMD ["bash", "/etc/nginx/start.sh"]
EXPOSE 80 443