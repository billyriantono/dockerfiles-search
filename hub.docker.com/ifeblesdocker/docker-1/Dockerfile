FROM nginx:1.15

ENV DIR /opt/project

RUN mkdir -p $DIR

COPY default.conf /etc/nginx/conf.d/default.conf

WORKDIR $DIR

COPY index.html .

EXPOSE 90/tcp

VOLUME $DIR

CMD ["nginx", "-g", "daemon off;"]
