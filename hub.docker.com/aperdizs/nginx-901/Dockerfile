FROM nginx:1.15.5

ARG workDir=/opt/project

ENV DIR $workDir
ENV USER docker

RUN mkdir -p $DIR
RUN groupadd $USER && useradd -g $USER $USER
RUN chown $USER:$USER $DIR

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY . $DIR

USER $USER

WORKDIR $DIR

EXPOSE 90/tcp
VOLUME $DIR

ENTRYPOINT ["nginx"]

CMD ["-g", "daemon off;"]