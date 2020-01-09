FROM centos:7.3.1611
MAINTAINER "Paul Allen" <paul@cloudcoreo.com>

USER root

ENV PYTHONPATH /usr/lib/python3.4/site-packages

RUN yum install -y https://centos7.iuscommunity.org/ius-release.rpm \
    && yum -y update && yum -y install wget which tar python34 python34-pip \
    && which python3.4 \
    && pip3.4 install requests \
    && yum clean all \
    && rm -rf /var/cache/yum/*

RUN export NVM_DIR="/root/.nvm" \
    && curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash \
    && echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm' >> /root/.bashrc \
    && source /root/.bashrc \
    && nvm install "7.8.0" \
    && nvm use --default "7.8.0"

RUN cd /tmp \
    && wget --no-check-certificate https://github.com/mitmproxy/mitmproxy/releases/download/v2.0.2/mitmproxy-2.0.2-linux.tar.gz \
    && tar -xvf mitmproxy-2.0.2-linux.tar.gz -C /usr/local/bin \
    && rm *mitm*

RUN rm -rf /opt/cloudcoreo/ \
    && mkdir -p /opt/cloudcoreo/proxy

COPY ./ /opt/cloudcoreo/proxy

RUN cd /opt/cloudcoreo/proxy \
    && source /root/.bashrc \
    && npm install

ENTRYPOINT [ "/bin/bash" ]

CMD [ "/opt/cloudcoreo/proxy/scripts/container_entry.sh" ]
