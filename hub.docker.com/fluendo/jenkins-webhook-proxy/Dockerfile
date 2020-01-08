from debian:stable
RUN apt-get update && apt-get install -y nginx apache2-utils procps
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 443
CMD ["nginx", "-g", "daemon off;"]
