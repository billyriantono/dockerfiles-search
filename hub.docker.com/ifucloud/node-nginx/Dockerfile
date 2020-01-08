FROM node:9

ENV APP_ROOT /var/www/site

RUN apt-get clean -y
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        nginx

EXPOSE 80 443

WORKDIR $APP_ROOT

CMD ["nginx", "-g", "daemon off;"]
