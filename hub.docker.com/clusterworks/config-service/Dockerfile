FROM centos:7

RUN yum -y install git make wget

# install n
WORKDIR /
RUN git clone https://github.com/tj/n.git \
    && cd n \
    && make \
    && make install \
    && cd .. \
    && rm -r n

# use n to install node
RUN n lts

# install config-service
RUN mkdir /config-service
COPY package.json /config-service/package.json
COPY service.js /config-service/service.js
RUN cd /config-service && npm install

# add the entry point
COPY entrypoint.sh /entrypoint.sh

EXPOSE 80/tcp

ENTRYPOINT ["/entrypoint.sh"]

CMD ["node", "/config-service/service.js", "/config.yml"]