FROM docker.io/node:6

RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && \
    apt-get -y update && \
    apt-get install -y ansible && \
    apt-get clean

WORKDIR /srv/nci-ansible-ui

ADD data /srv/nci-ansible-ui/data
COPY package.json /srv/nci-ansible-ui
RUN npm install

EXPOSE 3000

COPY entrypoint.sh /bin/entrypoint.sh
RUN chmod +x /bin/entrypoint.sh
ENTRYPOINT ["/bin/entrypoint.sh"]

CMD [ "node_modules/.bin/nci" ]
