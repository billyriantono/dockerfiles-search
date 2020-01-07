FROM nginx:1.13

COPY nginx.conf /etc/nginx/conf.d/default.conf

RUN apt-get -y update && apt-get install -y curl

#HEALTHCHECK --interval=1m --timeout=3s CMD curl --fail http://localhost/ || exit 1

