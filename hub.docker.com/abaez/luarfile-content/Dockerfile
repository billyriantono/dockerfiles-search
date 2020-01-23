FROM debian:latest
RUN apt-get update
RUN apt-get install -y nginx vim

ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
EXPOSE 80
