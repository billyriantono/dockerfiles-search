FROM debian:9.2

RUN apt-get update
RUN apt-get install -y rsync dos2unix nginx openssh-server vim sudo
RUN apt-get autoremove
RUN apt-get clean

ENV ROOT_DIR=/etc/i9corp/packages
ENV FREEBSD_DIR=${ROOT_DIR}/freebsd
ENV FREEBSD_ARM64=${FREEBSD_DIR}/arm64
ENV FREEBSD_AMD64=${FREEBSD_DIR}/amd64

COPY ./tools/start-packages /usr/local/bin/start-packages
RUN dos2unix /usr/local/bin/start-packages \
    && chmod +x /usr/local/bin/start-packages 

RUN mkdir -p ${FREEBSD_ARM64} ${FREEBSD_AMD64}
RUN mkdir -p .cache

ARG REPO_PASSWD=123456

COPY ./nginx/freebsd /etc/nginx/sites-available/freebsd

RUN unlink /etc/nginx/sites-enabled/default
RUN rm -fr /etc/nginx/sites-available/default
RUN ln -s /etc/nginx/sites-available/freebsd /etc/nginx/sites-enabled/default

RUN useradd -ms /bin/bash repo && echo "repo:${REPO_PASSWD}" | chpasswd

RUN chown -R repo:repo ${ROOT_DIR}

VOLUME [ "/etc/i9corp/packages/freebsd" ]

#Nginx
EXPOSE 80

#SSH
EXPOSE 22

CMD ["/usr/local/bin/start-packages"]
