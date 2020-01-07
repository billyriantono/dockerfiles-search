FROM nginx:1.9.6

MAINTAINER Aklis <aklis@qq.com>
#The php container is only to execute php script

COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/ /etc/nginx/conf.d/

# Add the support of redis and composer

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
