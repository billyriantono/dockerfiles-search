FROM centos:7

ADD scripts/setup.sh /usr/local/bin/setup
ADD scripts/download.sh /usr/local/bin/download

RUN /usr/local/bin/setup
ENV KUBERNETES_VERSION="1.12"

CMD [ "/usr/local/bin/download" ]
