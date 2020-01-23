FROM nginx:1.10
MAINTAINER Matteo Panella <matteo.panella@cnaf.infn.it>

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80 443 8443 9443

ENTRYPOINT ["nginx", "-g", "daemon off;"]
