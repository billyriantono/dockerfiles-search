FROM nginx:latest

COPY /conf/nginx.conf /etc/nginx/nginx.conf
ENV sb_port def_port_value
RUN sed -i "s#80#${sb_port}#g" /etc/nginx/nginx.conf
COPY /src /src
