FROM nginx:1.15.5

ENV DIR /opt/project

WORKDIR $DIR

RUN mkdir -p $DIR

COPY default.conf /etc/nginx/conf.d/default.conf
COPY index.html $DIR/index.html

EXPOSE 90/tcp

VOLUME $DIR

ENTRYPOINT [ "nginx", "-g", "daemon off;"]