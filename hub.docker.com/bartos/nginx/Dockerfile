FROM nginx
MAINTAINER Vojtech Bartos <docker@vojtechbartos.com>

RUN mkdir -p /project

RUN chown -R www-data:www-data /project
RUN chmod -R 777 /project

RUN rm /etc/nginx/conf.d/default.conf
RUN rm /etc/nginx/nginx.conf

WORKDIR /project

COPY ./project.conf /etc/nginx/conf.d/project.conf
COPY ./nginx.conf /etc/nginx/nginx.conf
