FROM ubuntu:14.04
RUN apt-get update 
RUN apt-get install -y nginx

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
