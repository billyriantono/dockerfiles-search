FROM nginx:1.13.0-alpine

ADD ./nginx.conf /etc/nginx/nginx.conf
ADD ./nginx-badbot-blocker/blacklist.conf /etc/nginx/blacklist.conf
ADD ./nginx-badbot-blocker/blockips.conf /etc/nginx/blockips.conf

CMD ["nginx", "-g", "daemon off; error_log stderr info;"]
