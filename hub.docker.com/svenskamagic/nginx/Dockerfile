FROM nginx:1.13.12

RUN apt-get update && apt-get install -y nano procps

COPY nginx.conf /etc/nginx/conf.d/default.conf
