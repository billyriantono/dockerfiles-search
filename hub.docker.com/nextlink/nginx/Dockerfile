FROM nginx

RUN apt-get update && apt-get -y install apache2-utils

COPY default.conf /etc/nginx/conf.d/default.conf
COPY init.sh /root/init.sh

ENTRYPOINT ["/root/init.sh"]
CMD ["nginx", "-g", "daemon off;"]
