FROM centos:latest
RUN yum install -y go \
                   make \
                   httpd-tools

ADD . /tmp
WORKDIR /tmp
RUN go run build.go
RUN /usr/bin/install -m 755 rest-server /usr/local/bin/rest-server
RUN make install && rm -rf *


RUN useradd -d /home/restic -m -s /bin/bash restic
RUN mkdir /data ; chown -R restic:restic /data

USER restic
WORKDIR /home/restic

ENV DATA_DIRECTORY /data
ENV PASSWORD_FILE /data/.htpasswd
RUN touch /data/.htpasswd

COPY docker/*_user /usr/bin/

VOLUME /data

EXPOSE 8000
EXPOSE 80

COPY docker/entrypoint.sh /entrypoint.sh

CMD [ "/entrypoint.sh" ]